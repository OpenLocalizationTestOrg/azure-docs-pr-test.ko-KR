---
title: "Azure Cosmos DB 규모 및 성능 테스트 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행하는 방법을 알아봅니다."
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="a49b5-104">Azure Cosmos DB를 사용한 성능 및 규모 테스트</span><span class="sxs-lookup"><span data-stu-id="a49b5-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="a49b5-105">성능 및 규모 테스트는 응용 프로그램 개발의 핵심 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="a49b5-106">대부분의 응용 프로그램에서 데이터베이스 계층은 전반적인 성능 및 확장성에 큰 영향을 미치므로 성능 테스트의 주요 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="a49b5-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 탄력적인 규모 및 예측 가능한 성능을 위해 작성되었으므로 고성능 데이터베이스 계층을 필요로 하는 응용 프로그램에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="a49b5-108">이 문서는 개발자가 자신의 Cosmos DB 작업에 대한 성능 테스트 모음을 구현하거나 Cosmos DB에서 고성능 응용 프로그램 시나리오를 평가할 때 참조로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="a49b5-109">또한 이 문서는 데이터베이스의 격리된 성능 테스트에 중점을 두지만 프로덕션 응용 프로그램에 대한 모범 사례도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="a49b5-110">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="a49b5-111">Cosmos DB의 성능 테스트를 위한 샘플 .NET 클라이언트 응용 프로그램은 어디에서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="a49b5-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="a49b5-112">클라이언트 응용 프로그램에서 Cosmos DB를 사용하여 높은 처리량 수준을 달성하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="a49b5-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="a49b5-113">코드를 시작하려면 [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)에서 프로젝트를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="a49b5-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="a49b5-114">이 응용 프로그램의 목표는 적은 수의 클라이언트 컴퓨터를 사용하여 Cosmos DB에서 더 나은 성능을 얻기 위한 모범 사례를 제시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="a49b5-115">제한 없이 확장할 수 있는 서비스의 최대 용량을 보여 주려는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="a49b5-116">Cosmos DB의 성능 향상을 위한 클라이언트 쪽 구성 옵션에 대한 자세한 내용은 [Azure Cosmos DB 성능 팁](performance-tips.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a49b5-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="a49b5-117">성능 테스트 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a49b5-117">Run the performance testing application</span></span>
<span data-ttu-id="a49b5-118">가장 빠른 시작 방법은 아래 단계에 설명된 대로 아래의 .NET 샘플을 컴파일하고 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="a49b5-119">소스 코드를 검토하고 자체 클라이언트 응용 프로그램에 대해 비슷한 구성을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="a49b5-120">**1단계:** [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)에서 프로젝트를 다운로드하거나 GitHub 리포지토리를 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="a49b5-121">**2단계:** App.config에서 EndpointUrl, AuthorizationKey, CollectionThroughput 및 DocumentTemplate(옵션)에 대한 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="a49b5-122">높은 처리량의 컬렉션을 프로비전하기 전에 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하여 컬렉션당 비용을 추정합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="a49b5-123">Azure Cosmos DB는 시간 단위로 저장소 및 처리량의 비용을 별도로 청구하므로 테스트 후에 Azure Cosmos DB 컬렉션을 삭제하거나 처리량을 줄여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="a49b5-124">**3단계:** 명령줄에서 콘솔 앱을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="a49b5-125">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-125">You should see output like the following:</span></span>

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


<span data-ttu-id="a49b5-126">**4단계(필요한 경우):** 도구에서 보고된 처리량(RU/s)은 컬렉션의 프로비전된 처리량과 같거나 많아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="a49b5-127">그렇지 않은 경우 DegreeOfParallelism을 조금씩 늘리면 제한에 도달하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="a49b5-128">클라이언트 앱의 처리량이 안정화될 경우 같거나 다른 컴퓨터에서 앱의 여러 인스턴스를 시작하면 여러 다른 인스턴스 간에 프로비전된 제한에 도달하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="a49b5-129">이 단계에 대해 도움이 필요한 경우 askcosmosdb@microsoft.com에 전자 메일을 보내거나 [Azure Portal](https://portal.azure.com)에서 지원 티켓을 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="a49b5-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a49b5-130">실행 중인 앱이 있는 경우 다양한 [인덱싱 정책](indexing-policies.md) 및 [일관성 수준](consistency-levels.md)을 시도하면서 처리량 및 대기 시간에 미치는 영향을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="a49b5-131">소스 코드를 검토하고 자체 테스트 제품군 또는 프로덕션 응용 프로그램에 대해 비슷한 구성을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49b5-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a49b5-132">Next steps</span></span>
<span data-ttu-id="a49b5-133">이 문서에서는 .NET 콘솔 앱을 사용하여 Cosmos DB로 성능 및 규모 테스트를 수행하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a49b5-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="a49b5-134">Azure Cosmos DB 사용 방법에 대한 자세한 내용은 아래 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a49b5-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="a49b5-135">Azure Cosmos DB 성능 테스트 샘플</span><span class="sxs-lookup"><span data-stu-id="a49b5-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="a49b5-136">Azure Cosmos DB 성능 향상을 위한 클라이언트 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="a49b5-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="a49b5-137">Azure Cosmos DB의 서버 쪽 분할</span><span class="sxs-lookup"><span data-stu-id="a49b5-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)



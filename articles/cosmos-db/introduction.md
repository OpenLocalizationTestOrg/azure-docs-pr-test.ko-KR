---
title: "Azure Cosmos DB 소개 | Microsoft Docs"
description: "Azure Cosmos DB에 대해 알아봅니다. 이 전세계에 배포된 멀티모델 데이터베이스는 낮은 대기 시간, 탄력적 확장성 및 고가용성을 위해 구축되었습니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: c9d04ae0bc11b99f893e5f003f136fbfe0dfccc9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="welcome-to-azure-cosmos-db"></a><span data-ttu-id="39e6f-104">Azure Cosmos DB 시작</span><span class="sxs-lookup"><span data-stu-id="39e6f-104">Welcome to Azure Cosmos DB</span></span>

<span data-ttu-id="39e6f-105">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 멀티모델 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-105">Azure Cosmos DB is Microsoft's globally distributed, multi-model database.</span></span> <span data-ttu-id="39e6f-106">Azure Cosmos DB에서는 단추를 클릭하는 간단한 방식으로 Azure의 지리적 위치 수에 관계없이 처리량 및 저장소를 탄력적 및 독립적으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-106">With the click of a button, Azure Cosmos DB enables you to elastically and independently scale throughput and storage across any number of Azure's geographic regions.</span></span> <span data-ttu-id="39e6f-107">다른 데이터베이스 서비스에서는 제공하지 않는 포괄적 [Service Level Agreement(서비스 수준 약정)](https://aka.ms/acdbsla)(SLA)를 통해 처리량, 대기 시간, 가용성 및 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-107">It offers throughput, latency, availability, and consistency guarantees with comprehensive [service level agreements](https://aka.ms/acdbsla) (SLAs), something no other database service can offer.</span></span>

![Azure Cosmos DB는 탄력적 확장, 낮은 대기 시간 보증, 일관성 모델 5개, 포괄적 보장 SLA를 갖춘 전세계에 배포된 데이터베이스 서비스입니다.](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a><span data-ttu-id="39e6f-109">Azure Cosmos DB를 활용하는 솔루션</span><span class="sxs-lookup"><span data-stu-id="39e6f-109">Solutions that benefit from Azure Cosmos DB</span></span>

<span data-ttu-id="39e6f-110">[전역적](distribute-data-globally.md)으로 짧은 응답 시간 내에 다양한 데이터에 대규모의 읽기 및 쓰기를 처리해야 하는 모든 [웹, 모바일, 게임 및 IoT 응용 프로그램](use-cases.md)은 Azure Cosmos DB의 [보장된](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 사용 가용성, 높은 처리량, 짧은 대기 시간 및 조정 가능한 일관성으로 인해 이익을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-110">Any [web, mobile, gaming, and IoT applications](use-cases.md) that need to handle massive amounts of reads and writes on a [global](distribute-data-globally.md) scale with low response times for a variety of data will benefit from Azure Cosmos DB's [guaranteed](https://azure.microsoft.com/support/legal/sla/cosmos-db/) availability, high throughput, low latency, and tunable consistency.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="39e6f-111">주요 기능</span><span class="sxs-lookup"><span data-stu-id="39e6f-111">Key capabilities</span></span>
<span data-ttu-id="39e6f-112">세계적으로 분산된 데이터베이스 서비스인 Azure Cosmos DB는 확장성 있고 응답성 높은 응용 프로그램을 빌드할 수 있도록 다음과 같은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-112">As a globally distributed database service, Azure Cosmos DB provides the following capabilities to help you build scalable, highly responsive applications:</span></span>

* <span data-ttu-id="39e6f-113">**턴키 글로벌 배포**</span><span class="sxs-lookup"><span data-stu-id="39e6f-113">**Turnkey global distribution**</span></span>
    * <span data-ttu-id="39e6f-114">[단추를 클릭](tutorial-global-distribution-documentdb.md)하여 원하는 수의 [Azure 지역](https://azure.microsoft.com/regions/)에 [데이터를 배포](distribute-data-globally.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-114">You can [distribute your data](distribute-data-globally.md) to any number of [Azure regions](https://azure.microsoft.com/regions/), with the [click of a button](tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="39e6f-115">이렇게 하면 사용자가 있는 위치에 데이터를 배치하여 고객에게 가장 짧을 대기 시간을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-115">This enables you to put your data where your users are, ensuring the lowest possible latency to your customers.</span></span> 
    * <span data-ttu-id="39e6f-116">앱에서는 Azure Cosmos DB의 멀티 호밍 API를 사용하여 가장 가까운 지역을 알고 가장 가까운 데이터 센터에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-116">Using Azure Cosmos DB's multi-homing APIs, the app always knows where the nearest region is and will send requests to the nearest data center.</span></span> <span data-ttu-id="39e6f-117">이 모든 작업은 구성을 변경하지 않고 수행할 수 있습니다. 쓰기 지역 및 읽기 지역을 원하는 만큼 설정하면 나머지도 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-117">All of this is possible with no config changes, you set your write region and as many read regions as you want and the rest is handled for you.</span></span>

* <span data-ttu-id="39e6f-118">**데이터 액세스 및 쿼리를 위한 다중 데이터 모델 및 주요 API**</span><span class="sxs-lookup"><span data-stu-id="39e6f-118">**Multiple data models and popular APIs for accessing and querying data**</span></span>
    * <span data-ttu-id="39e6f-119">Azure Cosmos DB를 빌드한 ARS(atom-record-sequence) 기반 데이터 모델은 문서, 그래프, 키-값, 테이블 및 열 형식 데이터 모델을 비롯한 다양한 데이터 모델을 고유하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-119">The atom-record-sequence (ARS) based data model that Azure Cosmos DB is built on natively supports multiple data models, including but not limited to document, graph, key-value, table, and columnar data models.</span></span>
    * <span data-ttu-id="39e6f-120">여러 언어에서 사용할 수 있는 SDK로 다음 데이터 모델의 API가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-120">APIs for the following data models are supported with SDKs available in multiple languages:</span></span>
        * [<span data-ttu-id="39e6f-121">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="39e6f-121">DocumentDB API</span></span>](documentdb-introduction.md)
        * [<span data-ttu-id="39e6f-122">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="39e6f-122">MongoDB API</span></span>](mongodb-introduction.md)
        * [<span data-ttu-id="39e6f-123">Table API</span><span class="sxs-lookup"><span data-stu-id="39e6f-123">Table API</span></span>](table-introduction.md)
        * [<span data-ttu-id="39e6f-124">Graph(Gremlin) API</span><span class="sxs-lookup"><span data-stu-id="39e6f-124">Graph (Gremlin) API</span></span>](graph-introduction.md)
        * <span data-ttu-id="39e6f-125">추가 데이터 모델 제공 예정</span><span class="sxs-lookup"><span data-stu-id="39e6f-125">Additional data models coming soon</span></span> 

* <span data-ttu-id="39e6f-126">**전세계에서 필요 시 탄력적으로 처리량 및 저장소 확장**</span><span class="sxs-lookup"><span data-stu-id="39e6f-126">**Elastically scale throughput and storage on demand, worldwide**</span></span>
    * <span data-ttu-id="39e6f-127">데이터베이스 처리량을 [초](request-units.md) 단위로 간편하게 확장하고 원하면 언제든 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-127">Easily scale database throughput at a [per second](request-units.md) granularity, and change it anytime you want.</span></span> 
    * <span data-ttu-id="39e6f-128">크기 요구 사항에 맞게 지속적으로 저장소 크기를 [투명하게 자동으로](partition-data.md) 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-128">Scale storage size [transparently and automatically](partition-data.md) to handle your size requirements now and forever.</span></span>

* <span data-ttu-id="39e6f-129">**응답성 높은 중요 업무용 응용 프로그램 빌드**</span><span class="sxs-lookup"><span data-stu-id="39e6f-129">**Build highly responsive and mission-critical applications**</span></span>
    * <span data-ttu-id="39e6f-130">Azure Cosmos DB는 고객에게 백분위 99의 종단 간 대기 시간을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-130">Azure Cosmos DB guarantees end-to-end low latency at the 99th percentile to its customers.</span></span> 
    * <span data-ttu-id="39e6f-131">일반적인 1KB 항목의 경우 Cosmos DB는 동일한 Azure 지역에서 백분위 99로 읽기 10ms 미만, 인덱스된 쓰기 15ms 미만의 종단 간 대기 시간을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-131">For a typical 1 KB item, Cosmos DB guarantees end-to-end latency of reads under 10 ms and indexed writes under 15 ms at the 99th percentile, within the same Azure region.</span></span> <span data-ttu-id="39e6f-132">중간 대기 시간이 크게 낮아집니다(5ms 미만).</span><span class="sxs-lookup"><span data-stu-id="39e6f-132">The median latencies are significantly lower (under 5 ms).</span></span>

* <span data-ttu-id="39e6f-133">**"Always On" 가용성 보장**</span><span class="sxs-lookup"><span data-stu-id="39e6f-133">**Ensure "always on" availability**</span></span>
    * <span data-ttu-id="39e6f-134">단일 지역 내에서 99.99%의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-134">99.99% availability within a single region.</span></span>
    * <span data-ttu-id="39e6f-135">원하는 만큼의 [Azure 지역](https://azure.microsoft.com/regions)에 배포하여 더 높은 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-135">Deploy to any number of [Azure regions](https://azure.microsoft.com/regions) for higher availability.</span></span>
    * <span data-ttu-id="39e6f-136">데이터 무손실 보장을 통해 하나 이상의 지역에서 [오류를 시뮬레이션](regional-failover.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-136">[Simulate a failure](regional-failover.md) of one or more regions with zero-data loss guarantees.</span></span> 

* <span data-ttu-id="39e6f-137">**올바른 방법으로 전세계에 배포되는 응용 프로그램 작성**</span><span class="sxs-lookup"><span data-stu-id="39e6f-137">**Write globally distributed applications, the right way**</span></span>
    * <span data-ttu-id="39e6f-138">다섯 가지 [일관성 모델](consistency-levels.md)은 항상 강력한 SQL 형태의 일관성과 NoSQL 형태의 결과적 일관성 및 그 중간 형태의 모든 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-138">Five [consistency models](consistency-levels.md) models provide a spectrum of strong SQL-like consistency all the way to NoSQL-like eventual consistency, and every thing in between.</span></span> 
  
* <span data-ttu-id="39e6f-139">**환불 보장**</span><span class="sxs-lookup"><span data-stu-id="39e6f-139">**Money back guarantees**</span></span>
    * <span data-ttu-id="39e6f-140">데이터를 빠르게 가져오지 않는다면 환불할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-140">Your data gets there fast, or your money back.</span></span> 
    * <span data-ttu-id="39e6f-141">가용성, 대기 시간, 처리량 및 일관성에 대한 [서비스 수준 계약](https://aka.ms/acdbsla) </span><span class="sxs-lookup"><span data-stu-id="39e6f-141">[Service level agreements](https://aka.ms/acdbsla) for availability, latency, throughput, and consistency.</span></span> 

* <span data-ttu-id="39e6f-142">**데이터베이스 스키마/인덱스 관리 없음**</span><span class="sxs-lookup"><span data-stu-id="39e6f-142">**No database schema/index management**</span></span>
    * <span data-ttu-id="39e6f-143">데이터베이스 스키마와 인덱스를 응용 프로그램의 스키마와 동기 상태로 유지하는 것에 대해 염려하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-143">Stop worrying about keeping your database schema and indexes in-sync with your application’s schema.</span></span> <span data-ttu-id="39e6f-144">이제 스키마 제약이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-144">We're schema-free.</span></span> 
    * <span data-ttu-id="39e6f-145">Azure Cosmos DB의 데이터베이스 엔진은 스키마에서 완전히 자유로우며 스키마나 인덱스 없이 자신이 수집한 모든 데이터를 자동으로 인덱싱하며 매우 빠르게 쿼리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-145">Azure Cosmos DB’s database engine is fully schema-agnostic – it automatically indexes all the data it ingests without requiring any schema or indexes and serves blazing fast queries.</span></span> 

* <span data-ttu-id="39e6f-146">**낮은 소유 비용**</span><span class="sxs-lookup"><span data-stu-id="39e6f-146">**Low cost of ownership**</span></span>
    * <span data-ttu-id="39e6f-147">비 관리 솔루션에 비해 5~10배 [비용 효과적](https://aka.ms/cosmos-db-tco-paper) </span><span class="sxs-lookup"><span data-stu-id="39e6f-147">Five to ten times [more cost effective](https://aka.ms/cosmos-db-tco-paper) than a non-managed solution.</span></span>
    * <span data-ttu-id="39e6f-148">DynamoDB보다 세 배 저렴합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-148">Three times cheaper than DynamoDB.</span></span>

## <a name="capability-comparison"></a><span data-ttu-id="39e6f-149">기능 비교</span><span class="sxs-lookup"><span data-stu-id="39e6f-149">Capability comparison</span></span>

<span data-ttu-id="39e6f-150">Azure Cosmos DB는 관계형 및 비관계형 데이터베이스의 최고 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-150">Azure Cosmos DB provides the best capabilities of relational and non-relational databases.</span></span>

| <span data-ttu-id="39e6f-151">기능</span><span class="sxs-lookup"><span data-stu-id="39e6f-151">Capabilities</span></span> | <span data-ttu-id="39e6f-152">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="39e6f-152">Relational databases</span></span>   | <span data-ttu-id="39e6f-153">비관계형(NoSQL) 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="39e6f-153">Non-relational (NoSQL) databases</span></span> |    <span data-ttu-id="39e6f-154">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="39e6f-154">Azure Cosmos DB</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39e6f-155">글로벌 분포</span><span class="sxs-lookup"><span data-stu-id="39e6f-155">Global distribution</span></span> | <span data-ttu-id="39e6f-156">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-156">No</span></span> | <span data-ttu-id="39e6f-157">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-157">No</span></span> | <span data-ttu-id="39e6f-158">예, 멀티 호밍 API를 사용하여 30개 이상의 지역에서 턴키 배포</span><span class="sxs-lookup"><span data-stu-id="39e6f-158">Yes, turnkey distribution in 30+ regions, with multi-homing APIs</span></span>|
| <span data-ttu-id="39e6f-159">수평적 확장</span><span class="sxs-lookup"><span data-stu-id="39e6f-159">Horizontal scale</span></span> | <span data-ttu-id="39e6f-160">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-160">No</span></span> | <span data-ttu-id="39e6f-161">예</span><span class="sxs-lookup"><span data-stu-id="39e6f-161">Yes</span></span> | <span data-ttu-id="39e6f-162">예, 독립적으로 저장소 및 처리량을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-162">Yes, you can independently scale storage and throughput</span></span> | 
| <span data-ttu-id="39e6f-163">대기 시간 보장</span><span class="sxs-lookup"><span data-stu-id="39e6f-163">Latency guarantees</span></span> | <span data-ttu-id="39e6f-164">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-164">No</span></span> | <span data-ttu-id="39e6f-165">예</span><span class="sxs-lookup"><span data-stu-id="39e6f-165">Yes</span></span> | <span data-ttu-id="39e6f-166">예, <10ms인 읽기의 99% 및 <15 ms인 쓰기</span><span class="sxs-lookup"><span data-stu-id="39e6f-166">Yes, 99% of reads in <10 ms and writes in <15 ms</span></span> | 
| <span data-ttu-id="39e6f-167">고가용성</span><span class="sxs-lookup"><span data-stu-id="39e6f-167">High availability</span></span> | <span data-ttu-id="39e6f-168">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-168">No</span></span> | <span data-ttu-id="39e6f-169">예</span><span class="sxs-lookup"><span data-stu-id="39e6f-169">Yes</span></span> | <span data-ttu-id="39e6f-170">예, Cosmos DB는 Always On이며 PACELC 장단점이 있고, 자동 및 수동 장애 조치 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39e6f-170">Yes, Cosmos DB is always on, has PACELC tradeoffs, and provides automatic & manual failover options</span></span>|
| <span data-ttu-id="39e6f-171">데이터 모델 + API</span><span class="sxs-lookup"><span data-stu-id="39e6f-171">Data model + API</span></span> | <span data-ttu-id="39e6f-172">관계형 + SQL</span><span class="sxs-lookup"><span data-stu-id="39e6f-172">Relational + SQL</span></span> | <span data-ttu-id="39e6f-173">다중 모델 + OSS API</span><span class="sxs-lookup"><span data-stu-id="39e6f-173">Multi-model + OSS API</span></span> | <span data-ttu-id="39e6f-174">다중 모델 + SQL + OSS API(추가 서비스 예정)</span><span class="sxs-lookup"><span data-stu-id="39e6f-174">Multi-model + SQL + OSS API (more coming soon)</span></span> |
| <span data-ttu-id="39e6f-175">SLA</span><span class="sxs-lookup"><span data-stu-id="39e6f-175">SLAs</span></span> | <span data-ttu-id="39e6f-176">예</span><span class="sxs-lookup"><span data-stu-id="39e6f-176">Yes</span></span> | <span data-ttu-id="39e6f-177">아니요</span><span class="sxs-lookup"><span data-stu-id="39e6f-177">No</span></span> | <span data-ttu-id="39e6f-178">예, 대기 시간, 처리량, 일관성, 가용성에 대한 포괄적 SLA</span><span class="sxs-lookup"><span data-stu-id="39e6f-178">Yes, comprehensive SLAs for latency, throughput, consistency, availability</span></span> |


## <a name="next-steps"></a><span data-ttu-id="39e6f-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39e6f-179">Next steps</span></span>
<span data-ttu-id="39e6f-180">다음 요약 설명서를 통해 Azure Cosmos DB를 시작해 보세요.</span><span class="sxs-lookup"><span data-stu-id="39e6f-180">Get started with Azure Cosmos DB with one of our quickstarts:</span></span>

* [<span data-ttu-id="39e6f-181">Azure Cosmos DB의 DocumentDB API 시작</span><span class="sxs-lookup"><span data-stu-id="39e6f-181">Get started with Azure Cosmos DB's DocumentDB API</span></span>](create-documentdb-dotnet.md)
* [<span data-ttu-id="39e6f-182">Azure Cosmos DB의 MongoDB API 시작</span><span class="sxs-lookup"><span data-stu-id="39e6f-182">Get started with Azure Cosmos DB's MongoDB API</span></span>](create-mongodb-nodejs.md)
* [<span data-ttu-id="39e6f-183">Azure Cosmos DB의 Graph API 시작</span><span class="sxs-lookup"><span data-stu-id="39e6f-183">Get started with Azure Cosmos DB's Graph API</span></span>](create-graph-dotnet.md)
* [<span data-ttu-id="39e6f-184">Azure Cosmos DB의 Table API 시작</span><span class="sxs-lookup"><span data-stu-id="39e6f-184">Get started with Azure Cosmos DB's Table API</span></span>](create-table-dotnet.md)

---
title: Cosmos DB aaaIntroduction tooAzure | Microsoft Docs
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
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a><span data-ttu-id="8e304-104">시작 tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8e304-104">Welcome tooAzure Cosmos DB</span></span>

<span data-ttu-id="8e304-105">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 멀티모델 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-105">Azure Cosmos DB is Microsoft's globally distributed, multi-model database.</span></span> <span data-ttu-id="8e304-106">Hello 단추 클릭으로 Azure Cosmos DB 있습니다 눈금 처리량 및 저장소 독립적으로 tooelastically 개수에 관계 없이 Azure의 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-106">With hello click of a button, Azure Cosmos DB enables you tooelastically and independently scale throughput and storage across any number of Azure's geographic regions.</span></span> <span data-ttu-id="8e304-107">다른 데이터베이스 서비스에서는 제공하지 않는 포괄적 [Service Level Agreement(서비스 수준 약정)](https://aka.ms/acdbsla)(SLA)를 통해 처리량, 대기 시간, 가용성 및 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-107">It offers throughput, latency, availability, and consistency guarantees with comprehensive [service level agreements](https://aka.ms/acdbsla) (SLAs), something no other database service can offer.</span></span>

![Azure Cosmos DB는 탄력적 확장, 낮은 대기 시간 보증, 일관성 모델 5개, 포괄적 보장 SLA를 갖춘 전세계에 배포된 데이터베이스 서비스입니다.](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a><span data-ttu-id="8e304-109">Azure Cosmos DB를 활용하는 솔루션</span><span class="sxs-lookup"><span data-stu-id="8e304-109">Solutions that benefit from Azure Cosmos DB</span></span>

<span data-ttu-id="8e304-110">모든 [웹, 모바일, 게임 및 응용 프로그램 IoT](use-cases.md) toohandle 대량의 읽기 및 쓰기에 필요한는 [글로벌](distribute-data-globally.md) Azure Cosmos DB에서 이익을 얻을 다양 한 데이터에 대 한 짧은 응답 시간 함께 크기 조정 [보장](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 가용성, 높은 처리량, 짧은 대기 시간 및 튜닝할 수 있는 일관성.</span><span class="sxs-lookup"><span data-stu-id="8e304-110">Any [web, mobile, gaming, and IoT applications](use-cases.md) that need toohandle massive amounts of reads and writes on a [global](distribute-data-globally.md) scale with low response times for a variety of data will benefit from Azure Cosmos DB's [guaranteed](https://azure.microsoft.com/support/legal/sla/cosmos-db/) availability, high throughput, low latency, and tunable consistency.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="8e304-111">주요 기능</span><span class="sxs-lookup"><span data-stu-id="8e304-111">Key capabilities</span></span>
<span data-ttu-id="8e304-112">전 세계적으로 분산된 데이터베이스 서비스로 Azure Cosmos DB 확장 가능한 응답성이 높은 응용 프로그램을 구축 하는 기능 toohelp 다음 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-112">As a globally distributed database service, Azure Cosmos DB provides hello following capabilities toohelp you build scalable, highly responsive applications:</span></span>

* <span data-ttu-id="8e304-113">**턴키 글로벌 배포**</span><span class="sxs-lookup"><span data-stu-id="8e304-113">**Turnkey global distribution**</span></span>
    * <span data-ttu-id="8e304-114">할 수 있습니다 [데이터 배포](distribute-data-globally.md) tooany 수가 [Azure 지역](https://azure.microsoft.com/regions/), hello로 [단추 클릭](tutorial-global-distribution-documentdb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-114">You can [distribute your data](distribute-data-globally.md) tooany number of [Azure regions](https://azure.microsoft.com/regions/), with hello [click of a button](tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="8e304-115">이렇게 하면 tooput 수 있는 사용자가 보장 hello 가장 낮은 대기 시간을 최소화 tooyour 고객 데이터.</span><span class="sxs-lookup"><span data-stu-id="8e304-115">This enables you tooput your data where your users are, ensuring hello lowest possible latency tooyour customers.</span></span> 
    * <span data-ttu-id="8e304-116">Azure Cosmos DB를 사용 하 여 멀티 호 밍 Api, hello 앱 항상 영역 가장 가까운 hello 이며 데이터 센터에 가장 가까운 요청 toohello 송신할 위치를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-116">Using Azure Cosmos DB's multi-homing APIs, hello app always knows where hello nearest region is and will send requests toohello nearest data center.</span></span> <span data-ttu-id="8e304-117">이 모든 가능한 구성 변경 없이 쓰기 지역 설정 있고, 원하는 고 hello 영역을 읽을 많은 rest 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-117">All of this is possible with no config changes, you set your write region and as many read regions as you want and hello rest is handled for you.</span></span>

* <span data-ttu-id="8e304-118">**데이터 액세스 및 쿼리를 위한 다중 데이터 모델 및 주요 API**</span><span class="sxs-lookup"><span data-stu-id="8e304-118">**Multiple data models and popular APIs for accessing and querying data**</span></span>
    * <span data-ttu-id="8e304-119">Azure Cosmos DB에 고유 하 게 작성 된 hello atom 레코드 시퀀스 (ARS) 기반된 데이터 모델에는 포함 하지만 제한 되지 toodocument, 그래프, 키-값, 테이블 및 칼럼 형식 데이터 모델의 여러 데이터 모델을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-119">hello atom-record-sequence (ARS) based data model that Azure Cosmos DB is built on natively supports multiple data models, including but not limited toodocument, graph, key-value, table, and columnar data models.</span></span>
    * <span data-ttu-id="8e304-120">여러 언어에서 사용할 수 있는 Sdk와 데이터 모델을 따르는 hello에 대 한 Api 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-120">APIs for hello following data models are supported with SDKs available in multiple languages:</span></span>
        * [<span data-ttu-id="8e304-121">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="8e304-121">DocumentDB API</span></span>](documentdb-introduction.md)
        * [<span data-ttu-id="8e304-122">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8e304-122">MongoDB API</span></span>](mongodb-introduction.md)
        * [<span data-ttu-id="8e304-123">Table API</span><span class="sxs-lookup"><span data-stu-id="8e304-123">Table API</span></span>](table-introduction.md)
        * [<span data-ttu-id="8e304-124">Graph(Gremlin) API</span><span class="sxs-lookup"><span data-stu-id="8e304-124">Graph (Gremlin) API</span></span>](graph-introduction.md)
        * <span data-ttu-id="8e304-125">추가 데이터 모델 제공 예정</span><span class="sxs-lookup"><span data-stu-id="8e304-125">Additional data models coming soon</span></span> 

* <span data-ttu-id="8e304-126">**전세계에서 필요 시 탄력적으로 처리량 및 저장소 확장**</span><span class="sxs-lookup"><span data-stu-id="8e304-126">**Elastically scale throughput and storage on demand, worldwide**</span></span>
    * <span data-ttu-id="8e304-127">데이터베이스 처리량을 [초](request-units.md) 단위로 간편하게 확장하고 원하면 언제든 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-127">Easily scale database throughput at a [per second](request-units.md) granularity, and change it anytime you want.</span></span> 
    * <span data-ttu-id="8e304-128">저장소 크기를 확장 [투명 하 고 자동으로](partition-data.md) toohandle 크기 요구 사항이 이제 하 고 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-128">Scale storage size [transparently and automatically](partition-data.md) toohandle your size requirements now and forever.</span></span>

* <span data-ttu-id="8e304-129">**응답성 높은 중요 업무용 응용 프로그램 빌드**</span><span class="sxs-lookup"><span data-stu-id="8e304-129">**Build highly responsive and mission-critical applications**</span></span>
    * <span data-ttu-id="8e304-130">Azure Cosmos DB 종단 간 대기 시간이 짧은 hello에 99th 백분위 수 tooits 고객을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-130">Azure Cosmos DB guarantees end-to-end low latency at hello 99th percentile tooits customers.</span></span> 
    * <span data-ttu-id="8e304-131">일반적인 1 KB 항목 Cosmos DB 보장 읽기의 종단 간 대기 시간이 10ms 미만 및 인덱싱된 쓰기 hello 99 번째 백분위 수에 15 밀리초 미만 내 동일 hello Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-131">For a typical 1 KB item, Cosmos DB guarantees end-to-end latency of reads under 10 ms and indexed writes under 15 ms at hello 99th percentile, within hello same Azure region.</span></span> <span data-ttu-id="8e304-132">hello 중앙값 대기 시간이 너무 지나치게 적으면 (아래에서 5 밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-132">hello median latencies are significantly lower (under 5 ms).</span></span>

* <span data-ttu-id="8e304-133">**"Always On" 가용성 보장**</span><span class="sxs-lookup"><span data-stu-id="8e304-133">**Ensure "always on" availability**</span></span>
    * <span data-ttu-id="8e304-134">단일 지역 내에서 99.99%의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-134">99.99% availability within a single region.</span></span>
    * <span data-ttu-id="8e304-135">Tooany 수의 배포 [Azure 지역](https://azure.microsoft.com/regions) 높은 가용성을 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-135">Deploy tooany number of [Azure regions](https://azure.microsoft.com/regions) for higher availability.</span></span>
    * <span data-ttu-id="8e304-136">데이터 무손실 보장을 통해 하나 이상의 지역에서 [오류를 시뮬레이션](regional-failover.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-136">[Simulate a failure](regional-failover.md) of one or more regions with zero-data loss guarantees.</span></span> 

* <span data-ttu-id="8e304-137">**전 세계적으로 분산된 응용 프로그램의 작성 hello 올바른 방법**</span><span class="sxs-lookup"><span data-stu-id="8e304-137">**Write globally distributed applications, hello right way**</span></span>
    * <span data-ttu-id="8e304-138">5 개의 [일관성 모델](consistency-levels.md) 모델은 다양 한 tooNoSQL와 비슷한 방식으로 결과적 일관성 및 사이 저것 hello 모두 강력한 SQL과 유사한 일관성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-138">Five [consistency models](consistency-levels.md) models provide a spectrum of strong SQL-like consistency all hello way tooNoSQL-like eventual consistency, and every thing in between.</span></span> 
  
* <span data-ttu-id="8e304-139">**환불 보장**</span><span class="sxs-lookup"><span data-stu-id="8e304-139">**Money back guarantees**</span></span>
    * <span data-ttu-id="8e304-140">데이터를 빠르게 가져오지 않는다면 환불할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-140">Your data gets there fast, or your money back.</span></span> 
    * <span data-ttu-id="8e304-141">가용성, 대기 시간, 처리량 및 일관성에 대한 [서비스 수준 계약](https://aka.ms/acdbsla) </span><span class="sxs-lookup"><span data-stu-id="8e304-141">[Service level agreements](https://aka.ms/acdbsla) for availability, latency, throughput, and consistency.</span></span> 

* <span data-ttu-id="8e304-142">**데이터베이스 스키마/인덱스 관리 없음**</span><span class="sxs-lookup"><span data-stu-id="8e304-142">**No database schema/index management**</span></span>
    * <span data-ttu-id="8e304-143">데이터베이스 스키마와 인덱스를 응용 프로그램의 스키마와 동기 상태로 유지하는 것에 대해 염려하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-143">Stop worrying about keeping your database schema and indexes in-sync with your application’s schema.</span></span> <span data-ttu-id="8e304-144">이제 스키마 제약이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-144">We're schema-free.</span></span> 
    * <span data-ttu-id="8e304-145">Azure Cosmos DB의 데이터베이스 엔진은 완전히 스키마를 알 수 없는 – 모든 hello 데이터 스키마 이나 인덱스 없이 수집 하 고 매우 빠른 쿼리 사용을 자동으로 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-145">Azure Cosmos DB’s database engine is fully schema-agnostic – it automatically indexes all hello data it ingests without requiring any schema or indexes and serves blazing fast queries.</span></span> 

* <span data-ttu-id="8e304-146">**낮은 소유 비용**</span><span class="sxs-lookup"><span data-stu-id="8e304-146">**Low cost of ownership**</span></span>
    * <span data-ttu-id="8e304-147">5 tooten 번 [비용 효율이](https://aka.ms/cosmos-db-tco-paper) 관리 되지 않는 솔루션 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-147">Five tooten times [more cost effective](https://aka.ms/cosmos-db-tco-paper) than a non-managed solution.</span></span>
    * <span data-ttu-id="8e304-148">DynamoDB보다 세 배 저렴합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-148">Three times cheaper than DynamoDB.</span></span>

## <a name="capability-comparison"></a><span data-ttu-id="8e304-149">기능 비교</span><span class="sxs-lookup"><span data-stu-id="8e304-149">Capability comparison</span></span>

<span data-ttu-id="8e304-150">Azure Cosmos DB hello 비관계형 및 관계형 데이터베이스의 가장 뛰어난 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-150">Azure Cosmos DB provides hello best capabilities of relational and non-relational databases.</span></span>

| <span data-ttu-id="8e304-151">기능</span><span class="sxs-lookup"><span data-stu-id="8e304-151">Capabilities</span></span> | <span data-ttu-id="8e304-152">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8e304-152">Relational databases</span></span>   | <span data-ttu-id="8e304-153">비관계형(NoSQL) 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8e304-153">Non-relational (NoSQL) databases</span></span> |    <span data-ttu-id="8e304-154">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8e304-154">Azure Cosmos DB</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e304-155">글로벌 분포</span><span class="sxs-lookup"><span data-stu-id="8e304-155">Global distribution</span></span> | <span data-ttu-id="8e304-156">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-156">No</span></span> | <span data-ttu-id="8e304-157">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-157">No</span></span> | <span data-ttu-id="8e304-158">예, 멀티 호밍 API를 사용하여 30개 이상의 지역에서 턴키 배포</span><span class="sxs-lookup"><span data-stu-id="8e304-158">Yes, turnkey distribution in 30+ regions, with multi-homing APIs</span></span>|
| <span data-ttu-id="8e304-159">수평적 확장</span><span class="sxs-lookup"><span data-stu-id="8e304-159">Horizontal scale</span></span> | <span data-ttu-id="8e304-160">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-160">No</span></span> | <span data-ttu-id="8e304-161">예</span><span class="sxs-lookup"><span data-stu-id="8e304-161">Yes</span></span> | <span data-ttu-id="8e304-162">예, 독립적으로 저장소 및 처리량을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-162">Yes, you can independently scale storage and throughput</span></span> | 
| <span data-ttu-id="8e304-163">대기 시간 보장</span><span class="sxs-lookup"><span data-stu-id="8e304-163">Latency guarantees</span></span> | <span data-ttu-id="8e304-164">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-164">No</span></span> | <span data-ttu-id="8e304-165">예</span><span class="sxs-lookup"><span data-stu-id="8e304-165">Yes</span></span> | <span data-ttu-id="8e304-166">예, <10ms인 읽기의 99% 및 <15 ms인 쓰기</span><span class="sxs-lookup"><span data-stu-id="8e304-166">Yes, 99% of reads in <10 ms and writes in <15 ms</span></span> | 
| <span data-ttu-id="8e304-167">고가용성</span><span class="sxs-lookup"><span data-stu-id="8e304-167">High availability</span></span> | <span data-ttu-id="8e304-168">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-168">No</span></span> | <span data-ttu-id="8e304-169">예</span><span class="sxs-lookup"><span data-stu-id="8e304-169">Yes</span></span> | <span data-ttu-id="8e304-170">예, Cosmos DB는 Always On이며 PACELC 장단점이 있고, 자동 및 수동 장애 조치 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e304-170">Yes, Cosmos DB is always on, has PACELC tradeoffs, and provides automatic & manual failover options</span></span>|
| <span data-ttu-id="8e304-171">데이터 모델 + API</span><span class="sxs-lookup"><span data-stu-id="8e304-171">Data model + API</span></span> | <span data-ttu-id="8e304-172">관계형 + SQL</span><span class="sxs-lookup"><span data-stu-id="8e304-172">Relational + SQL</span></span> | <span data-ttu-id="8e304-173">다중 모델 + OSS API</span><span class="sxs-lookup"><span data-stu-id="8e304-173">Multi-model + OSS API</span></span> | <span data-ttu-id="8e304-174">다중 모델 + SQL + OSS API(추가 서비스 예정)</span><span class="sxs-lookup"><span data-stu-id="8e304-174">Multi-model + SQL + OSS API (more coming soon)</span></span> |
| <span data-ttu-id="8e304-175">SLA</span><span class="sxs-lookup"><span data-stu-id="8e304-175">SLAs</span></span> | <span data-ttu-id="8e304-176">예</span><span class="sxs-lookup"><span data-stu-id="8e304-176">Yes</span></span> | <span data-ttu-id="8e304-177">아니요</span><span class="sxs-lookup"><span data-stu-id="8e304-177">No</span></span> | <span data-ttu-id="8e304-178">예, 대기 시간, 처리량, 일관성, 가용성에 대한 포괄적 SLA</span><span class="sxs-lookup"><span data-stu-id="8e304-178">Yes, comprehensive SLAs for latency, throughput, consistency, availability</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8e304-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e304-179">Next steps</span></span>
<span data-ttu-id="8e304-180">다음 요약 설명서를 통해 Azure Cosmos DB를 시작해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8e304-180">Get started with Azure Cosmos DB with one of our quickstarts:</span></span>

* [<span data-ttu-id="8e304-181">Azure Cosmos DB의 DocumentDB API 시작</span><span class="sxs-lookup"><span data-stu-id="8e304-181">Get started with Azure Cosmos DB's DocumentDB API</span></span>](create-documentdb-dotnet.md)
* [<span data-ttu-id="8e304-182">Azure Cosmos DB의 MongoDB API 시작</span><span class="sxs-lookup"><span data-stu-id="8e304-182">Get started with Azure Cosmos DB's MongoDB API</span></span>](create-mongodb-nodejs.md)
* [<span data-ttu-id="8e304-183">Azure Cosmos DB의 Graph API 시작</span><span class="sxs-lookup"><span data-stu-id="8e304-183">Get started with Azure Cosmos DB's Graph API</span></span>](create-graph-dotnet.md)
* [<span data-ttu-id="8e304-184">Azure Cosmos DB의 Table API 시작</span><span class="sxs-lookup"><span data-stu-id="8e304-184">Get started with Azure Cosmos DB's Table API</span></span>](create-table-dotnet.md)

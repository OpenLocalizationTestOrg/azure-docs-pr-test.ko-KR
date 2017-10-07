---
title: "키 값 저장소 – 비용 개요로 Cosmos DB aaaAzure | Microsoft Docs"
description: "키 값 저장소로 Azure Cosmos DB를 사용 하 여 hello 낮은 비용에 알아봅니다."
keywords: "키 값 저장소"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a><span data-ttu-id="97f9f-104">키 값 저장소로서의 Azure Cosmos DB – 비용 개요</span><span class="sxs-lookup"><span data-stu-id="97f9f-104">Azure Cosmos DB as a key value store – Cost overview</span></span>

<span data-ttu-id="97f9f-105">Azure Cosmos DB는 대규모의 고가용성 응용 프로그램을 쉽게 빌드하기 위한 전역으로 분산된 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-105">Azure Cosmos DB is a globally distributed, multi-model database service for building highly available, large scale applications easily.</span></span> <span data-ttu-id="97f9f-106">기본적으로 Azure Cosmos DB 효율적으로 수집 하는 모든 hello 데이터를 자동으로 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-106">By default, Azure Cosmos DB automatically indexes all hello data it ingests, efficiently.</span></span> <span data-ttu-id="97f9f-107">이를 통해 모든 종류의 데이터에 대해 빠르고 일관된 [SQL](documentdb-sql-query.md)(및 [JavaScript](programming.md)) 쿼리가 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-107">This enables fast and consistent [SQL](documentdb-sql-query.md) (and [JavaScript](programming.md)) queries on any kind of data.</span></span> 

<span data-ttu-id="97f9f-108">이 문서는 간단한 쓰기를 위해 Azure Cosmos DB의 hello 비용에 설명 하 고 키/값 저장소로 사용 될 때 읽기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-108">This article describes hello cost of Azure Cosmos DB for simple write and read operations when it’s used as a key/value store.</span></span> <span data-ttu-id="97f9f-109">쓰기 작업에는 문서의 삽입, 바꾸기, 삭제 및 upsert가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-109">Write operations include inserts, replaces, deletes, and upserts of documents.</span></span> <span data-ttu-id="97f9f-110">99.99% 가용성을 보장 하는 것 외에도 Azure Cosmos DB 제공 보장 < 읽기에 대 한 대기 시간이 10ms 및 < (인덱싱된) hello에 대 한 대기 시간이 15 밀리초 hello 99 번째 백분위 수에 각각 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-110">Besides guaranteeing 99.99% high availability, Azure Cosmos DB offers guaranteed <10 ms latency for reads and <15 ms latency for hello (indexed) writes respectively, at hello 99th percentile.</span></span> 

## <a name="why-we-use-request-units-rus"></a><span data-ttu-id="97f9f-111">RU(요청 단위)를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="97f9f-111">Why we use Request Units (RUs)</span></span>

<span data-ttu-id="97f9f-112">Azure DB Cosmos 성능 hello 양을 기반 프로 비전 된 [요청 단위](request-units.md) (RU) hello 파티션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-112">Azure Cosmos DB performance is based on hello amount of provisioned [Request Units](request-units.md) (RU) for hello partition.</span></span> <span data-ttu-id="97f9f-113">두 번째 세분성에 있고 RUs/sec 및 RUs/min 구입한 hello를 프로 비전 ([toobe 시간별 청구 hello와 혼동된 하지](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span><span class="sxs-lookup"><span data-stu-id="97f9f-113">hello provisioning is at a second granularity and is purchased in RUs/sec and RUs/min ([not toobe confused with hello hourly billing](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span></span> <span data-ttu-id="97f9f-114">RUs는 hello 프로 비전 hello 응용 프로그램에 필요한 처리량을 간소화 하는 통화로 고려 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-114">RUs should be considered as a currency that simplifies hello provisioning of required throughput for hello application.</span></span> <span data-ttu-id="97f9f-115">고객을 구별 toothink 읽기 및 쓰기 용량 단위 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-115">Our customers do not have toothink of differentiating between read and write capacity units.</span></span> <span data-ttu-id="97f9f-116">RUs의 hello 단일 동시성 모델 읽기와 쓰기 간의 tooshare hello를 프로 비전 된 용량 효율성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-116">hello single currency model of RUs creates efficiencies tooshare hello provisioned capacity between reads and writes.</span></span> <span data-ttu-id="97f9f-117">이 프로 비전 된 용량이 모델 hello 서비스 tooprovide를 예측 가능 하 고 일관 된 처리량, 짧은 대기 시간 및 고가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-117">This provisioned capacity model enables hello service tooprovide a predictable and consistent throughput, guaranteed low latency, and high availability.</span></span> <span data-ttu-id="97f9f-118">마지막으로, RU toomodel 처리량 사용 하는 각 프로 비전 된 RU에도 정의 된 리소스 (메모리, 코어).</span><span class="sxs-lookup"><span data-stu-id="97f9f-118">Finally, we use RU toomodel throughput but each provisioned RU has also a defined amount of resources (Memory, Core).</span></span> <span data-ttu-id="97f9f-119">초당 RU는 IOPS만이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-119">RU/sec is not only IOPS.</span></span>

<span data-ttu-id="97f9f-120">전 세계적으로 분산된 데이터베이스 시스템으로 Cosmos DB 추가 toohigh 가용성의 대기 시간, 처리량 및 일관성에 SLA를 제공 하는 Azure 서비스만을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-120">As a globally distributed database system, Cosmos DB is hello only Azure service that provides an SLA on latency, throughput, and consistency in addition toohigh availability.</span></span> <span data-ttu-id="97f9f-121">프로 비전 하는 hello 처리량은 적용 된 tooeach Cosmos DB 데이터베이스 계정에 연결 된 hello 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-121">hello throughput you provision is applied tooeach of hello regions associated with your Cosmos DB database account.</span></span> <span data-ttu-id="97f9f-122">읽기에 대 한 Cosmos DB 제공 잘 정의 된 여러 [일관성 수준](consistency-levels.md) 에서 toochoose에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-122">For reads, Cosmos DB offers multiple, well-defined [consistency levels](consistency-levels.md) for you toochoose from.</span></span> 

<span data-ttu-id="97f9f-123">hello 다음 표에 나와 hello RUs 필요한 tooperform 읽기 수 및 1KB에서 100KBs의 문서 크기에 따라 트랜잭션을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-123">hello following table shows hello number of RUs required tooperform read and write transactions based on document size of 1KB and 100KBs.</span></span>

|<span data-ttu-id="97f9f-124">항목 크기</span><span class="sxs-lookup"><span data-stu-id="97f9f-124">Item Size</span></span>|<span data-ttu-id="97f9f-125">1 읽기</span><span class="sxs-lookup"><span data-stu-id="97f9f-125">1 Read</span></span>|<span data-ttu-id="97f9f-126">1 쓰기</span><span class="sxs-lookup"><span data-stu-id="97f9f-126">1 Write</span></span>|
|-------------|------|-------|
|<span data-ttu-id="97f9f-127">1KB</span><span class="sxs-lookup"><span data-stu-id="97f9f-127">1 KB</span></span>|<span data-ttu-id="97f9f-128">1RU</span><span class="sxs-lookup"><span data-stu-id="97f9f-128">1 RU</span></span>|<span data-ttu-id="97f9f-129">5RU</span><span class="sxs-lookup"><span data-stu-id="97f9f-129">5 RUs</span></span>|
|<span data-ttu-id="97f9f-130">100KB</span><span class="sxs-lookup"><span data-stu-id="97f9f-130">100 KB</span></span>|<span data-ttu-id="97f9f-131">10RU</span><span class="sxs-lookup"><span data-stu-id="97f9f-131">10 RUs</span></span>|<span data-ttu-id="97f9f-132">50RU</span><span class="sxs-lookup"><span data-stu-id="97f9f-132">50 RUs</span></span>|

## <a name="cost-of-reads-and-writes"></a><span data-ttu-id="97f9f-133">읽기 및 쓰기의 비용</span><span class="sxs-lookup"><span data-stu-id="97f9f-133">Cost of Reads and writes</span></span>

<span data-ttu-id="97f9f-134">1, 000 RU/sec를 프로 비전 하면 too3.6m RU/시간 금액이 고 $0.08 hello 시간 (미국 hello와 유럽에서 일)에 대 한 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-134">If you provision 1,000 RU/sec, this amounts too3.6m RU/hour and will cost $0.08 for hello hour (in hello US and Europe).</span></span> <span data-ttu-id="97f9f-135">1KB 크기 문서에서는 프로비전된 처리량을 사용해서 3.6m 읽기 또는 0.72m 쓰기(초당 3.6m RU/5)를 사용할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-135">For a 1KB size document, this means that you can consume 3.6m reads or 0.72m writes (3.6mRU / 5) using your provisioned throughput.</span></span> <span data-ttu-id="97f9f-136">정규화 된 toomillion 읽기 및 쓰기, hello 비용 $0.022 /m 읽기 수 ($0.08 3.6 /) 및 $0.111/m 쓰기 ($0.08 0.72 /).</span><span class="sxs-lookup"><span data-stu-id="97f9f-136">Normalized toomillion reads and writes, hello cost would be $0.022 /m reads ($0.08 / 3.6) and $0.111/m writes ($0.08 / 0.72).</span></span> <span data-ttu-id="97f9f-137">hello 당 비용 백만 hello 테이블 아래에 나와 있는 것 처럼 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-137">hello cost per million becomes minimal as shown in hello table below.</span></span>

|<span data-ttu-id="97f9f-138">항목 크기</span><span class="sxs-lookup"><span data-stu-id="97f9f-138">Item Size</span></span>|<span data-ttu-id="97f9f-139">1m 읽기</span><span class="sxs-lookup"><span data-stu-id="97f9f-139">1m Read</span></span>|<span data-ttu-id="97f9f-140">1m 쓰기</span><span class="sxs-lookup"><span data-stu-id="97f9f-140">1m Write</span></span>|
|-------------|-------|--------|
|<span data-ttu-id="97f9f-141">1KB</span><span class="sxs-lookup"><span data-stu-id="97f9f-141">1 KB</span></span>|<span data-ttu-id="97f9f-142">$0.022</span><span class="sxs-lookup"><span data-stu-id="97f9f-142">$0.022</span></span>|<span data-ttu-id="97f9f-143">$0.111</span><span class="sxs-lookup"><span data-stu-id="97f9f-143">$0.111</span></span>|
|<span data-ttu-id="97f9f-144">100KB</span><span class="sxs-lookup"><span data-stu-id="97f9f-144">100 KB</span></span>|<span data-ttu-id="97f9f-145">$0.222</span><span class="sxs-lookup"><span data-stu-id="97f9f-145">$0.222</span></span>|<span data-ttu-id="97f9f-146">$1.111</span><span class="sxs-lookup"><span data-stu-id="97f9f-146">$1.111</span></span>|


<span data-ttu-id="97f9f-147">대부분의 hello 기본 blob 또는 백만 읽기 트랜잭션 및 $5 백만 쓰기 트랜잭션당 당 개체 저장소 서비스 요금이 $0.40 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-147">Most of hello basic blob or object stores services charge $0.40 per million read transaction and $5 per million write transaction.</span></span> <span data-ttu-id="97f9f-148">최적으로 사용 하는 경우 Cosmos DB too98 %1KB 트랜잭션 위해 이러한 다른 솔루션 보다 더 적게 듭니다 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-148">If used optimally, Cosmos DB can be up too98% cheaper than these other solutions (for 1KB transactions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97f9f-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97f9f-149">Next steps</span></span>

<span data-ttu-id="97f9f-150">Azure Cosmos DB 리소스 프로비저닝 최적화에 대한 새 문서를 계속 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="97f9f-150">Stay tuned for new articles on optimizing Azure Cosmos DB resource provisioning.</span></span> <span data-ttu-id="97f9f-151">에 가능한 toouse 느껴집니다 그 동안 hello 우리의 [RU 계산기](https://www.documentdb.com/capacityplanner)합니다.</span><span class="sxs-lookup"><span data-stu-id="97f9f-151">In hello meantime, feel free toouse our [RU calculator](https://www.documentdb.com/capacityplanner).</span></span>


---
title: "키 값 저장소로서의 Azure Cosmos DB – 비용 개요 | Microsoft Docs"
description: "Azure Cosmos DB를 키 값 저장소로 사용할 경우의 비용 절감 효과에 대해 알아봅니다."
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
ms.openlocfilehash: 33eef1b51a5ee00b0fa67096030ed9ce92cf768e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a><span data-ttu-id="07d80-104">키 값 저장소로서의 Azure Cosmos DB – 비용 개요</span><span class="sxs-lookup"><span data-stu-id="07d80-104">Azure Cosmos DB as a key value store – Cost overview</span></span>

<span data-ttu-id="07d80-105">Azure Cosmos DB는 대규모의 고가용성 응용 프로그램을 쉽게 빌드하기 위한 전역으로 분산된 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-105">Azure Cosmos DB is a globally distributed, multi-model database service for building highly available, large scale applications easily.</span></span> <span data-ttu-id="07d80-106">기본적으로 Azure Cosmos DB는 수집하는 모든 데이터를 자동으로 효율적으로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-106">By default, Azure Cosmos DB automatically indexes all the data it ingests, efficiently.</span></span> <span data-ttu-id="07d80-107">이를 통해 모든 종류의 데이터에 대해 빠르고 일관된 [SQL](documentdb-sql-query.md)(및 [JavaScript](programming.md)) 쿼리가 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-107">This enables fast and consistent [SQL](documentdb-sql-query.md) (and [JavaScript](programming.md)) queries on any kind of data.</span></span> 

<span data-ttu-id="07d80-108">이 문서는 키/값 저장소로 사용될 경우 간단한 쓰기 및 읽기 작업의 Azure Cosmos DB 비용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-108">This article describes the cost of Azure Cosmos DB for simple write and read operations when it’s used as a key/value store.</span></span> <span data-ttu-id="07d80-109">쓰기 작업에는 문서의 삽입, 바꾸기, 삭제 및 upsert가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-109">Write operations include inserts, replaces, deletes, and upserts of documents.</span></span> <span data-ttu-id="07d80-110">Azure Cosmos DB는 99.99%의 높은 가용성을 보장하는 것 외에, 99번째 백분위수로 읽기에 대해 10ms 미만의 대기 시간, (인덱싱된) 쓰기에 대해 15ms 미만의 대기 시간을 각각 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-110">Besides guaranteeing 99.99% high availability, Azure Cosmos DB offers guaranteed <10 ms latency for reads and <15 ms latency for the (indexed) writes respectively, at the 99th percentile.</span></span> 

## <a name="why-we-use-request-units-rus"></a><span data-ttu-id="07d80-111">RU(요청 단위)를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="07d80-111">Why we use Request Units (RUs)</span></span>

<span data-ttu-id="07d80-112">Azure Cosmos DB 성능은 파티션에 대해 프로비전된 RU([요청 단위](request-units.md)) 크기를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-112">Azure Cosmos DB performance is based on the amount of provisioned [Request Units](request-units.md) (RU) for the partition.</span></span> <span data-ttu-id="07d80-113">프로비전은 초 단위이며 초당 RU 및 분당 RU 단위로 구입합니다([시간별 청구와 혼동하지 말 것](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span><span class="sxs-lookup"><span data-stu-id="07d80-113">The provisioning is at a second granularity and is purchased in RUs/sec and RUs/min ([not to be confused with the hourly billing](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span></span> <span data-ttu-id="07d80-114">RU는 응용 프로그램의 필수 처리량 프로비전을 간소화하는 통화로 간주되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-114">RUs should be considered as a currency that simplifies the provisioning of required throughput for the application.</span></span> <span data-ttu-id="07d80-115">고객은 읽기 및 쓰기 용량 단위 간을 구분해서 생각할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-115">Our customers do not have to think of differentiating between read and write capacity units.</span></span> <span data-ttu-id="07d80-116">단일 통화 모델의 RU를 사용하면 읽기 및 쓰기 간에 프로비전된 용량을 효율적으로 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-116">The single currency model of RUs creates efficiencies to share the provisioned capacity between reads and writes.</span></span> <span data-ttu-id="07d80-117">이러한 프로비전된 용량 모델을 사용하면 서비스는 짧은 대기 시간 및 높은 가용성이 보장되는 예측 가능하고 일관된 처리량을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-117">This provisioned capacity model enables the service to provide a predictable and consistent throughput, guaranteed low latency, and high availability.</span></span> <span data-ttu-id="07d80-118">마지막으로 RU를 사용하여 처리량을 모델링하지만 프로비전된 각 RU에는 정의된 양의 리소스(메모리, 코어)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-118">Finally, we use RU to model throughput but each provisioned RU has also a defined amount of resources (Memory, Core).</span></span> <span data-ttu-id="07d80-119">초당 RU는 IOPS만이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-119">RU/sec is not only IOPS.</span></span>

<span data-ttu-id="07d80-120">전역적으로 분산된 데이터베이스 시스템인 Cosmos DB는 고가용성 외에 대기 시간, 처리량 및 일관성에 대한 SLA를 제공하는 유일한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-120">As a globally distributed database system, Cosmos DB is the only Azure service that provides an SLA on latency, throughput, and consistency in addition to high availability.</span></span> <span data-ttu-id="07d80-121">프로비전하는 처리량은 Cosmos DB 데이터베이스 계정에 연결된 각 하위 지역에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-121">The throughput you provision is applied to each of the regions associated with your Cosmos DB database account.</span></span> <span data-ttu-id="07d80-122">읽기의 경우 Cosmos DB는 선택 가능한 여러 개의 잘 정의된 [일관성 수준](consistency-levels.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-122">For reads, Cosmos DB offers multiple, well-defined [consistency levels](consistency-levels.md) for you to choose from.</span></span> 

<span data-ttu-id="07d80-123">다음 표에는 1KB 및 100KB 문서 크기에 따라 읽기 및 쓰기 트랜잭션을 수행하는 데 필요한 RU 수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-123">The following table shows the number of RUs required to perform read and write transactions based on document size of 1KB and 100KBs.</span></span>

|<span data-ttu-id="07d80-124">항목 크기</span><span class="sxs-lookup"><span data-stu-id="07d80-124">Item Size</span></span>|<span data-ttu-id="07d80-125">1 읽기</span><span class="sxs-lookup"><span data-stu-id="07d80-125">1 Read</span></span>|<span data-ttu-id="07d80-126">1 쓰기</span><span class="sxs-lookup"><span data-stu-id="07d80-126">1 Write</span></span>|
|-------------|------|-------|
|<span data-ttu-id="07d80-127">1KB</span><span class="sxs-lookup"><span data-stu-id="07d80-127">1 KB</span></span>|<span data-ttu-id="07d80-128">1RU</span><span class="sxs-lookup"><span data-stu-id="07d80-128">1 RU</span></span>|<span data-ttu-id="07d80-129">5RU</span><span class="sxs-lookup"><span data-stu-id="07d80-129">5 RUs</span></span>|
|<span data-ttu-id="07d80-130">100KB</span><span class="sxs-lookup"><span data-stu-id="07d80-130">100 KB</span></span>|<span data-ttu-id="07d80-131">10RU</span><span class="sxs-lookup"><span data-stu-id="07d80-131">10 RUs</span></span>|<span data-ttu-id="07d80-132">50RU</span><span class="sxs-lookup"><span data-stu-id="07d80-132">50 RUs</span></span>|

## <a name="cost-of-reads-and-writes"></a><span data-ttu-id="07d80-133">읽기 및 쓰기의 비용</span><span class="sxs-lookup"><span data-stu-id="07d80-133">Cost of Reads and writes</span></span>

<span data-ttu-id="07d80-134">초당 1,000RU를 프로비전하는 시간당 3.6m RU에 해당하며 시간당 $0.08가 됩니다(미국 및 유럽).</span><span class="sxs-lookup"><span data-stu-id="07d80-134">If you provision 1,000 RU/sec, this amounts to 3.6m RU/hour and will cost $0.08 for the hour (in the US and Europe).</span></span> <span data-ttu-id="07d80-135">1KB 크기 문서에서는 프로비전된 처리량을 사용해서 3.6m 읽기 또는 0.72m 쓰기(초당 3.6m RU/5)를 사용할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-135">For a 1KB size document, this means that you can consume 3.6m reads or 0.72m writes (3.6mRU / 5) using your provisioned throughput.</span></span> <span data-ttu-id="07d80-136">1백만 읽기 및 쓰기로 정규화할 경우 비용은 m 읽기당 $0.022($0.08/3.6) 및 m 쓰기당 $0.111($0.08/0.72)에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-136">Normalized to million reads and writes, the cost would be $0.022 /m reads ($0.08 / 3.6) and $0.111/m writes ($0.08 / 0.72).</span></span> <span data-ttu-id="07d80-137">백만당 비용은 아래 표에 나와 있는 것처럼 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-137">The cost per million becomes minimal as shown in the table below.</span></span>

|<span data-ttu-id="07d80-138">항목 크기</span><span class="sxs-lookup"><span data-stu-id="07d80-138">Item Size</span></span>|<span data-ttu-id="07d80-139">1m 읽기</span><span class="sxs-lookup"><span data-stu-id="07d80-139">1m Read</span></span>|<span data-ttu-id="07d80-140">1m 쓰기</span><span class="sxs-lookup"><span data-stu-id="07d80-140">1m Write</span></span>|
|-------------|-------|--------|
|<span data-ttu-id="07d80-141">1KB</span><span class="sxs-lookup"><span data-stu-id="07d80-141">1 KB</span></span>|<span data-ttu-id="07d80-142">$0.022</span><span class="sxs-lookup"><span data-stu-id="07d80-142">$0.022</span></span>|<span data-ttu-id="07d80-143">$0.111</span><span class="sxs-lookup"><span data-stu-id="07d80-143">$0.111</span></span>|
|<span data-ttu-id="07d80-144">100KB</span><span class="sxs-lookup"><span data-stu-id="07d80-144">100 KB</span></span>|<span data-ttu-id="07d80-145">$0.222</span><span class="sxs-lookup"><span data-stu-id="07d80-145">$0.222</span></span>|<span data-ttu-id="07d80-146">$1.111</span><span class="sxs-lookup"><span data-stu-id="07d80-146">$1.111</span></span>|


<span data-ttu-id="07d80-147">대부분의 기본 Blob 또는 개체 저장소 서비스는 백만 읽기 트랜잭션당 $0.40, 백만 쓰기 트랜잭션당 $5가 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d80-147">Most of the basic blob or object stores services charge $0.40 per million read transaction and $5 per million write transaction.</span></span> <span data-ttu-id="07d80-148">최적으로 사용하는 경우 Cosmos DB는 이러한 다른 솔루션보다 최대 98% 더 저렴할 수 있습니다(1KB 트랜잭션에 대해).</span><span class="sxs-lookup"><span data-stu-id="07d80-148">If used optimally, Cosmos DB can be up to 98% cheaper than these other solutions (for 1KB transactions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d80-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07d80-149">Next steps</span></span>

<span data-ttu-id="07d80-150">Azure Cosmos DB 리소스 프로비저닝 최적화에 대한 새 문서를 계속 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="07d80-150">Stay tuned for new articles on optimizing Azure Cosmos DB resource provisioning.</span></span> <span data-ttu-id="07d80-151">당분간은 [RU 계산기](https://www.documentdb.com/capacityplanner)를 무료로 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="07d80-151">In the meantime, feel free to use our [RU calculator](https://www.documentdb.com/capacityplanner).</span></span>


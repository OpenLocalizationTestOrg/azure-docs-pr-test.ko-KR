---
title: "DocumentDB API 성능 수준 | Microsoft Docs"
description: "DocumentDB API 성능 수준을 통해 컨테이너별 기준에 따라 처리량을 예약하는 방법을 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d4733e57eb760dbb8e8ca96f6ba55671d1742f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="c08ea-103">S1, S2 및 S3 성능 수준 사용 중지</span><span class="sxs-lookup"><span data-stu-id="c08ea-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c08ea-104">이 문서에서 설명하는 S1, S2 및 S3 성능 수준은 이제 사용 중지되어 새 DocumentDB API 계정에 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="c08ea-105">이 문서에서는 S1, S2 및 S3 성능 수준에 대한 개요를 간략히 설명하고, 이러한 성능 수준을 사용하는 컬렉션을 2017년 8월 1일부터 단일 파티션 컬렉션으로 마이그레이션하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="c08ea-106">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="c08ea-107">S1, S2 및 S3 성능 수준의 사용이 중지되는 이유는?</span><span class="sxs-lookup"><span data-stu-id="c08ea-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="c08ea-108">단일 파티션 컬렉션 및 분할된 컬렉션을 S1, S2, S3 성능 수준과 비교하면 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="c08ea-109">내 데이터에 중단 없이 액세스하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="c08ea-110">마이그레이션하면 내 컬렉션이 어떻게 변경됩니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="c08ea-111">단일 파티션 컬렉션으로 마이그레이션하면 요금 청구는 어떻게 변경됩니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="c08ea-112">저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="c08ea-113">2017년 8월 1일 이전의 S1, S2 및 S3 성능 수준을 변경할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="c08ea-114">내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="c08ea-115">S1, S2, S3 성능 수준에서 단일 파티션 컬렉션으로 마이그레이션하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="c08ea-116">EA 고객에게 미치는 영향은?</span><span class="sxs-lookup"><span data-stu-id="c08ea-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="c08ea-117">S1, S2 및 S3 성능 수준의 사용이 중지되는 이유는?</span><span class="sxs-lookup"><span data-stu-id="c08ea-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="c08ea-118">S1, S2 및 S3 성능 수준은 DocumentDB API 컬렉션에서 제공하는 유연성을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="c08ea-119">S1, S2, S3 성능 수준에서는 처리량과 저장소 용량이 둘 다 미리 설정되었으며 탄력성을 제공하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="c08ea-120">이제 Azure Cosmos DB는 처리량과 저장소를 사용자 지정할 수 있는 기능을 제공하므로 크기 조정 기능을 필요에 따라 훨씬 더 유연하게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-120">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="c08ea-121">단일 파티션 컬렉션 및 분할된 컬렉션을 S1, S2, S3 성능 수준과 비교하면 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="c08ea-122">다음 표에서는 단일 파티션 컬렉션, 분할된 컬렉션 및 S1, S2, S3 성능 수준에서 사용할 수 있는 처리량 및 저장소 옵션을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="c08ea-123">다음은 미국 동부 2 지역의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="c08ea-124">분할된 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c08ea-124">Partitioned collection</span></span>|<span data-ttu-id="c08ea-125">단일 파티션 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c08ea-125">Single partition collection</span></span>|<span data-ttu-id="c08ea-126">S1</span><span class="sxs-lookup"><span data-stu-id="c08ea-126">S1</span></span>|<span data-ttu-id="c08ea-127">S2</span><span class="sxs-lookup"><span data-stu-id="c08ea-127">S2</span></span>|<span data-ttu-id="c08ea-128">S3</span><span class="sxs-lookup"><span data-stu-id="c08ea-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="c08ea-129">최대 처리량</span><span class="sxs-lookup"><span data-stu-id="c08ea-129">Maximum throughput</span></span>|<span data-ttu-id="c08ea-130">Unlimited</span><span class="sxs-lookup"><span data-stu-id="c08ea-130">Unlimited</span></span>|<span data-ttu-id="c08ea-131">10,000RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-131">10K RU/s</span></span>|<span data-ttu-id="c08ea-132">250RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-132">250 RU/s</span></span>|<span data-ttu-id="c08ea-133">1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-133">1 K RU/s</span></span>|<span data-ttu-id="c08ea-134">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="c08ea-135">최소 처리량</span><span class="sxs-lookup"><span data-stu-id="c08ea-135">Minimum throughput</span></span>|<span data-ttu-id="c08ea-136">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-136">2.5K RU/s</span></span>|<span data-ttu-id="c08ea-137">400RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-137">400 RU/s</span></span>|<span data-ttu-id="c08ea-138">250RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-138">250 RU/s</span></span>|<span data-ttu-id="c08ea-139">1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-139">1 K RU/s</span></span>|<span data-ttu-id="c08ea-140">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="c08ea-141">최대 저장소</span><span class="sxs-lookup"><span data-stu-id="c08ea-141">Maximum storage</span></span>|<span data-ttu-id="c08ea-142">Unlimited</span><span class="sxs-lookup"><span data-stu-id="c08ea-142">Unlimited</span></span>|<span data-ttu-id="c08ea-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-143">10 GB</span></span>|<span data-ttu-id="c08ea-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-144">10 GB</span></span>|<span data-ttu-id="c08ea-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-145">10 GB</span></span>|<span data-ttu-id="c08ea-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-146">10 GB</span></span>|
|<span data-ttu-id="c08ea-147">가격(월별)</span><span class="sxs-lookup"><span data-stu-id="c08ea-147">Price (monthly)</span></span>|<span data-ttu-id="c08ea-148">처리량: $6/100RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="c08ea-149">저장소: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="c08ea-150">처리량: $6/100RU/s</span><span class="sxs-lookup"><span data-stu-id="c08ea-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="c08ea-151">저장소: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="c08ea-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="c08ea-152">$25(미화)</span><span class="sxs-lookup"><span data-stu-id="c08ea-152">$25 USD</span></span>|<span data-ttu-id="c08ea-153">$50(미화)</span><span class="sxs-lookup"><span data-stu-id="c08ea-153">$50 USD</span></span>|<span data-ttu-id="c08ea-154">$100(미화)</span><span class="sxs-lookup"><span data-stu-id="c08ea-154">$100 USD</span></span>|

<span data-ttu-id="c08ea-155">EA 고객입니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-155">Are you an EA customer?</span></span> <span data-ttu-id="c08ea-156">그렇다면 [EA 고객에게 미치는 영향은?](#ea-customer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="c08ea-157">내 데이터에 중단 없이 액세스하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="c08ea-158">아무 작업도 수행할 필요 없이 Cosmos DB에서 전적으로 마이그레이션을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-158">Nothing, Cosmos DB handles the migration for you.</span></span> <span data-ttu-id="c08ea-159">S1, S2 또는 S3 컬렉션이 있는 경우 현재 컬렉션은 2017년 7월 31일부터 단일 파티션 컬렉션으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="c08ea-160">마이그레이션하면 내 컬렉션이 어떻게 변경됩니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="c08ea-161">S1 컬렉션이 있는 경우 400RU/s 처리량의 단일 파티션 컬렉션으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="c08ea-162">400RU/s는 단일 파티션 컬렉션에서 사용할 수 있는 최소 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="c08ea-163">그러나 400RU/s 단일 파티션 컬렉션에 대한 비용은 250RU/s S1 컬렉션에 지불한 비용과 거의 동일하며, 사용 가능한 여분의 150RU/s에 대해 지불하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="c08ea-164">S2 컬렉션이 있는 경우 1,000RU/s 단일 파티션 컬렉션으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="c08ea-165">처리량 수준은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="c08ea-166">S3 컬렉션이 있는 경우 2,500RU/s 단일 파티션 컬렉션으로 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="c08ea-167">처리량 수준은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="c08ea-168">이러한 각각의 경우에서 컬렉션을 마이그레이션한 후에는 처리량 수준을 사용자 지정하거나 필요에 따라 크기를 조정하여 대기 시간이 짧은 액세스를 사용자에게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="c08ea-169">컬렉션을 마이그레이션한 후에 처리량 수준을 변경하려면 Azure Portal에서 Cosmos DB 계정을 열고 [크기 조정]을 클릭한 다음 컬렉션을 선택하고 다음 스크린샷과 같이 처리량 수준을 조정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-169">To change the throughput level after your collection has migrated, simply open your Cosmos DB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![Azure Portal에서 처리량을 조정하는 방법](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="c08ea-171">단일 파티션 컬렉션으로 마이그레이션한 후 요금 청구는 어떻게 변경됩니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="c08ea-172">미국 동부 지역에 각각 10개의 S1 컬렉션(각각 1GB 저장소 사용)이 있고, 이러한 10개 S1 컬렉션을 400RU/s(최소 수준)의 10개 단일 파티션 컬렉션으로 마이그레이션한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="c08ea-173">한 달 동안 10개의 단일 파티션 컬렉션을 유지하는 경우 청구서는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![10개 S1 컬렉션 및 10개 단일 파티션 컬렉션에 대한 가격 비교](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="c08ea-175">저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="c08ea-176">S1, S2 또는 S3 성능 수준 컬렉션 또는 단일 파티션 컬렉션이 있든 간에 모두 10GB 저장소를 사용할 수 있는 경우 Cosmos DB 데이터 마이그레이션 도구를 사용하여 거의 무제한 저장소가 있는 분할된 컬렉션으로 데이터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="c08ea-177">분할된 컬렉션의 이점에 대한 자세한 내용은 [Azure Cosmos DB의 분할 및 크기 조정](documentdb-partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="c08ea-178">S1, S2, S3 또는 단일 파티션 컬렉션을 분할된 컬렉션으로 마이그레이션하는 방법에 대한 내용은 [단일 파티션에서 분할된 컬렉션으로 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="c08ea-179">2017년 8월 1일 이전의 S1, S2 및 S3 성능 수준을 변경할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="c08ea-180">S1, S2 및 S3 성능을 갖춘 기존 계정만 포털을 통하거나 프로그래밍 방식으로 성능 수준 계층을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="c08ea-181">S1, S2 및 S3 성능 수준은 2017년 8월 1일 이후로 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="c08ea-182">S1, S3 또는 S3에서 단일 파티션 컬렉션으로 변경하면 S1, S2 또는 S3 성능 수준으로 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="c08ea-183">내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="c08ea-184">마이그레이션은 2017년 7월 31일부로 시행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="c08ea-185">S1, S2 또는 S3 성능 수준을 사용하는 컬렉션이 있는 경우 마이그레이션을 수행하기 전에 Cosmos DB 팀에서 메일로 연락을 드립니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-185">If you have a collection that uses the S1, S2 or S3 performance levels, the Cosmos DB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="c08ea-186">마이그레이션이 완료되면 2017년 8월 1일 Azure Portal에서 컬렉션에 표준 가격 정책이 적용되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![표준 가격 책정 계층으로 마이그레이션된 컬렉션을 확인하는 방법](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="c08ea-188">S1, S2, S3 성능 수준에서 단일 파티션 컬렉션으로 마이그레이션하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c08ea-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="c08ea-189">Azure Portal을 사용하거나 프로그래밍 방식으로 S1, S2 및 S3 성능 수준에서 단일 파티션 컬렉션으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="c08ea-190">8월 1일 이전에 이 작업을 직접 수행하여 단일 파티션 컬렉션에서 사용할 수 있는 유연한 처리량 옵션을 활용할 수 있거나 2017년 7월 31일에 사용자를 위해 컬렉션을 마이그레이션할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="c08ea-191">**Azure Portal을 사용하여 단일 파티션 컬렉션으로 마이그레이션하려면**</span><span class="sxs-lookup"><span data-stu-id="c08ea-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="c08ea-192">[**Azure Portal**](https://portal.azure.com)에서 **Azure Cosmos DB**를 클릭한 다음 수정할 Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-192">In the [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select the Cosmos DB account to modify.</span></span> 
 
    <span data-ttu-id="c08ea-193">**Azure Cosmos DB**가 이동 표시줄에 없는 경우 >를 클릭하고 **데이터베이스**까지 스크롤한 다음 **Azure Cosmos DB**, DocumentDB 계정을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-193">If **Azure Cosmos DB** is not on the Jumpbar, click >, scroll to **Databases**, select **Azure Cosmos DB**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="c08ea-194">리소스 메뉴의 **컨테이너** 아래에서 **규모**를 클릭하고 드롭다운 목록에서 수정할 컬렉션을 선택한 다음 **가격 책정 계층**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-194">On the resource menu, under **Containers**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="c08ea-195">미리 정의된 처리량을 사용하는 계정은 S1, S2 또는 S3의 가격 책정 계층을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="c08ea-196">**가격 책정 계층 선택** 블레이드에서 **표준**을 클릭하여 사용자 정의 처리량을 변경한 다음 **선택**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![처리량 값을 변경하는 위치를 보여 주는 설정 블레이드의 스크린 샷](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="c08ea-198">**규모** 블레이드로 돌아가면 **가격 책정 계층**이 **표준**으로 변경되어 있으며 **처리량(RU/s)** 상자에 기본값인 400이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="c08ea-199">처리량을 400~10,000개 RU/s( [요청 단위](request-units.md)/초) 사이로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-199">Set the throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="c08ea-200">월별 예상 비용을 제공하기 위해 페이지 아래쪽의 **월별 예상 비용**이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="c08ea-201">변경 내용을 저장하고 표준 가격 책정 계층으로 이동하면 S1, S2 또는 S3 성능 수준으로 롤백할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="c08ea-202">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="c08ea-203">더 많은 처리량(10,000RU/s 초과) 또는 더 많은 저장소(10GB 초과)가 필요하다고 판단되는 경우 분할된 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="c08ea-204">단일 파티션 컬렉션을 분할된 컬렉션으로 마이그레이션하려면 [단일 파티션에서 분할된 컬렉션으로 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c08ea-205">S1, S2 또는 S3에서 표준 계층으로 변경하는 데에는 최대 2분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="c08ea-206">**.NET SDK를 사용하여 단일 파티션 컬렉션으로 마이그레이션하려면**</span><span class="sxs-lookup"><span data-stu-id="c08ea-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="c08ea-207">컬렉션의 성능 수준 변경에 대한 다른 옵션은 SDK를 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="c08ea-208">이 섹션에서는 [DocumentDB .NET API](documentdb-sdk-dotnet.md)를 사용한 컬렉션의 성능 수준 변경에 대해서만 다루고 있으나, 다른 SDK의 경우에도 프로세스는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="c08ea-209">다음 코드 조각에서는 컬렉션 처리량을 5,000RU/s로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-209">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="c08ea-210">offer 메서드에 대한 자세한 내용 및 추가 예제를 보려면 [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="c08ea-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="c08ea-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="c08ea-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="c08ea-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="c08ea-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="c08ea-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="c08ea-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="c08ea-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="c08ea-215">EA 고객에게 미치는 영향은?</span><span class="sxs-lookup"><span data-stu-id="c08ea-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="c08ea-216">EA 고객에게 적용한 가격은 현재 계약이 종료될 때까지 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-216">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c08ea-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c08ea-217">Next steps</span></span>
<span data-ttu-id="c08ea-218">Azure Cosmos DB의 가격 책정 및 데이터 관리에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c08ea-218">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="c08ea-219">[Cosmos DB의 데이터 분할](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="c08ea-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="c08ea-220">단일 파티션 컨테이너와 분할된 컨테이너 간의 차이점을 이해하고 매끄럽게 크기를 조정하는 분할 전략을 구현하는 데 유용한 팁을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-220">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="c08ea-221">[Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c08ea-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="c08ea-222">처리량 프로비전 및 저장소 소비 비용에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-222">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="c08ea-223">[요청 단위](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="c08ea-223">[Request units](request-units.md).</span></span> <span data-ttu-id="c08ea-224">읽기, 쓰기, 쿼리와 같은 다양한 작업 유형의 처리량 사용에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c08ea-224">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>

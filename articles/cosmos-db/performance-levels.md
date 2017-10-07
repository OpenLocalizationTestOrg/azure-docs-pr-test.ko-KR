---
title: "API aaaDocumentDB 성능 수준 | Microsoft Docs"
description: "어떻게 DocumentDB API 성능 수준을 사용 하면 컨테이너 당 기준 tooreserve 처리량에 알아봅니다."
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
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="ca96f-103">Hello S1, S2, S3 성능 수준에 사용 중지</span><span class="sxs-lookup"><span data-stu-id="ca96f-103">Retiring hello S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ca96f-104">hello S1, S2, S3 성능 수준이이 문서에 설명 된 사용이 중지 되는 및 새 DocumentDB API 계정에 대해 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-104">hello S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="ca96f-105">이 문서에서는 S1, S2, S3 성능 수준에 대해 간략하게 설명 하 고 이러한 성능 수준을 사용 하는 hello 컬렉션 되는 방식이 마이그레이션된 toosingle 파티션 컬렉션 2017 년 8 월 1 일에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how hello collections that use these performance levels will be migrated toosingle partition collections on August 1st, 2017.</span></span> <span data-ttu-id="ca96f-106">이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-106">After reading this article, you'll be able tooanswer hello following questions:</span></span>

- [<span data-ttu-id="ca96f-107">이유는 hello S1, S2, S3 성능 수준을 사용이 중지 되 고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-107">Why are hello S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="ca96f-108">단일 파티션 컬렉션 및 분할 된 컬렉션 비교 하면 어떻게 toohello S1, S2, S3 성능 수준을?</span><span class="sxs-lookup"><span data-stu-id="ca96f-108">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="ca96f-109">작업 중단 없이 toodo tooensure toomy 데이터에 액세스할 필요?</span><span class="sxs-lookup"><span data-stu-id="ca96f-109">What do I need toodo tooensure uninterrupted access toomy data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="ca96f-110">Hello 마이그레이션 후 내 컬렉션은 어떻게 변경 됩니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-110">How will my collection change after hello migration?</span></span>](#collection-change)
- [<span data-ttu-id="ca96f-111">어떻게 청구 내 변경 마이그레이션된 toosingle 파티션 컬렉션 난 후?</span><span class="sxs-lookup"><span data-stu-id="ca96f-111">How will my billing change after I’m migrated toosingle partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="ca96f-112">저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="ca96f-113">2017 년 8 월 1 하기 전에 hello S1, S2, S3 성능 수준 간에 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ca96f-113">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="ca96f-114">내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="ca96f-115">Hello S1, S2, S3 성능 수준 toosingle 파티션 컬렉션 직접에서 마이그레이션하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-115">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="ca96f-116">EA 고객에게 미치는 영향은?</span><span class="sxs-lookup"><span data-stu-id="ca96f-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="ca96f-117">이유는 hello S1, S2, S3 성능 수준을 사용이 중지 되 고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-117">Why are hello S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="ca96f-118">hello S1, S2, S3 성능 수준 하지 제공 hello 유연성을 DocumentDB API 컬렉션에서 제공 하는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-118">hello S1, S2, and S3 performance levels do not offer hello flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="ca96f-119">Hello S1, S2, S3 성능 수준으로 두 hello 처리량 및 저장소 용량 미리 설정한 및 탄력성을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-119">With hello S1, S2, S3 performance levels, both hello throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="ca96f-120">Azure Cosmos DB 이제 제공 hello 기능 toocustomize 처리량 및 저장소를 필요에 따라 기능 tooscale에 훨씬 더 많은 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-120">Azure Cosmos DB now offers hello ability toocustomize your throughput and storage, offering you much more flexibility in your ability tooscale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a><span data-ttu-id="ca96f-121">단일 파티션 컬렉션 및 분할 된 컬렉션 비교 하면 어떻게 toohello S1, S2, S3 성능 수준을?</span><span class="sxs-lookup"><span data-stu-id="ca96f-121">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="ca96f-122">다음 표에서 hello 단일 파티션 컬렉션, 분할 된 컬렉션 및 S1, S2, S3 성능 수준에서 제공 하는 hello 처리량 및 저장소 옵션을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-122">hello following table compares hello throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="ca96f-123">다음은 미국 동부 2 지역의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="ca96f-124">분할된 컬렉션</span><span class="sxs-lookup"><span data-stu-id="ca96f-124">Partitioned collection</span></span>|<span data-ttu-id="ca96f-125">단일 파티션 컬렉션</span><span class="sxs-lookup"><span data-stu-id="ca96f-125">Single partition collection</span></span>|<span data-ttu-id="ca96f-126">S1</span><span class="sxs-lookup"><span data-stu-id="ca96f-126">S1</span></span>|<span data-ttu-id="ca96f-127">S2</span><span class="sxs-lookup"><span data-stu-id="ca96f-127">S2</span></span>|<span data-ttu-id="ca96f-128">S3</span><span class="sxs-lookup"><span data-stu-id="ca96f-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="ca96f-129">최대 처리량</span><span class="sxs-lookup"><span data-stu-id="ca96f-129">Maximum throughput</span></span>|<span data-ttu-id="ca96f-130">Unlimited</span><span class="sxs-lookup"><span data-stu-id="ca96f-130">Unlimited</span></span>|<span data-ttu-id="ca96f-131">10,000RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-131">10K RU/s</span></span>|<span data-ttu-id="ca96f-132">250RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-132">250 RU/s</span></span>|<span data-ttu-id="ca96f-133">1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-133">1 K RU/s</span></span>|<span data-ttu-id="ca96f-134">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="ca96f-135">최소 처리량</span><span class="sxs-lookup"><span data-stu-id="ca96f-135">Minimum throughput</span></span>|<span data-ttu-id="ca96f-136">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-136">2.5K RU/s</span></span>|<span data-ttu-id="ca96f-137">400RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-137">400 RU/s</span></span>|<span data-ttu-id="ca96f-138">250RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-138">250 RU/s</span></span>|<span data-ttu-id="ca96f-139">1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-139">1 K RU/s</span></span>|<span data-ttu-id="ca96f-140">2,500RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="ca96f-141">최대 저장소</span><span class="sxs-lookup"><span data-stu-id="ca96f-141">Maximum storage</span></span>|<span data-ttu-id="ca96f-142">Unlimited</span><span class="sxs-lookup"><span data-stu-id="ca96f-142">Unlimited</span></span>|<span data-ttu-id="ca96f-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-143">10 GB</span></span>|<span data-ttu-id="ca96f-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-144">10 GB</span></span>|<span data-ttu-id="ca96f-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-145">10 GB</span></span>|<span data-ttu-id="ca96f-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-146">10 GB</span></span>|
|<span data-ttu-id="ca96f-147">가격(월별)</span><span class="sxs-lookup"><span data-stu-id="ca96f-147">Price (monthly)</span></span>|<span data-ttu-id="ca96f-148">처리량: $6/100RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="ca96f-149">저장소: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="ca96f-150">처리량: $6/100RU/s</span><span class="sxs-lookup"><span data-stu-id="ca96f-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="ca96f-151">저장소: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="ca96f-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="ca96f-152">$25(미화)</span><span class="sxs-lookup"><span data-stu-id="ca96f-152">$25 USD</span></span>|<span data-ttu-id="ca96f-153">$50(미화)</span><span class="sxs-lookup"><span data-stu-id="ca96f-153">$50 USD</span></span>|<span data-ttu-id="ca96f-154">$100(미화)</span><span class="sxs-lookup"><span data-stu-id="ca96f-154">$100 USD</span></span>|

<span data-ttu-id="ca96f-155">EA 고객입니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-155">Are you an EA customer?</span></span> <span data-ttu-id="ca96f-156">그렇다면 [EA 고객에게 미치는 영향은?](#ea-customer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca96f-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a><span data-ttu-id="ca96f-157">작업 중단 없이 toodo tooensure toomy 데이터에 액세스할 필요?</span><span class="sxs-lookup"><span data-stu-id="ca96f-157">What do I need toodo tooensure uninterrupted access toomy data?</span></span>

<span data-ttu-id="ca96f-158">Nothing 이면 Cosmos DB 수에 대 한 hello 마이그레이션 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-158">Nothing, Cosmos DB handles hello migration for you.</span></span> <span data-ttu-id="ca96f-159">S1, S2 또는 S3 컬렉션을 설정한 경우 사용자의 현재 컬렉션 마이그레이션된 tooa 단일 파티션 컬렉션에 2017 년 7 월 31 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-159">If you have an S1, S2, or S3 collection, your current collection will be migrated tooa single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a><span data-ttu-id="ca96f-160">Hello 마이그레이션 후 내 컬렉션은 어떻게 변경 됩니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-160">How will my collection change after hello migration?</span></span>

<span data-ttu-id="ca96f-161">S1 컬렉션을 사용 하는 경우 400 000RU/s 처리량을 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-161">If you have an S1 collection, you will be migrated tooa single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="ca96f-162">400RU/s은 단일 파티션 컬렉션으로 사용할 수 있는 가장 낮은 처리량 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-162">400 RU/s is hello lowest throughput available with single partition collections.</span></span> <span data-ttu-id="ca96f-163">그러나 단일 파티션 컬렉션은 지불 동일 S1 컬렉션으로 된 hello 약 hello에 400RU/s 및 250 000RU/s – 하지에 대 한 지불 하 게는 하므로 hello 비용이 추가 150 000RU/s 사용 가능한 tooyou를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-163">However, hello cost for 400 RU/s in hello a single partition collection is approximately hello same as you were paying with your S1 collection and 250 RU/s – so you are not paying for hello extra 150 RU/s available tooyou.</span></span>

<span data-ttu-id="ca96f-164">S2 컬렉션을 사용 하는 경우 1, 000RU/s를 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-164">If you have an S2 collection, you will be migrated tooa single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="ca96f-165">변경 tooyour 처리량 수준이 없는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-165">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="ca96f-166">S3 컬렉션을 사용 하는 경우, 000RU/s 2.5를 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-166">If you have an S3 collection, you will be migrated tooa single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="ca96f-167">변경 tooyour 처리량 수준이 없는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-167">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="ca96f-168">각각의이 경우에 컬렉션 마이그레이션된 후를 수 수 toocustomize 처리량 수준을 아니면 필요한 tooprovide 대기 시간이 짧은 액세스 tooyour 사용자로 확장 및 축소 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-168">In each of these cases, after your collection is migrated, you will be able toocustomize your throughput level, or scale it up and down as needed tooprovide low-latency access tooyour users.</span></span> <span data-ttu-id="ca96f-169">toochange hello 처리량 수준 컬렉션을 마이그레이션한 후 단순히 Cosmos DB 계정을 열고 hello Azure 포털에서에서 배율, 컬렉션을 선택를 hello 스크린 샷 다음 그림과 같이 hello 처리량 수준을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-169">toochange hello throughput level after your collection has migrated, simply open your Cosmos DB account in hello Azure portal, click Scale, choose your collection, and then adjust hello throughput level, as shown in hello following screenshot:</span></span>

![어떻게 tooscale 처리량 hello Azure 포털](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a><span data-ttu-id="ca96f-171">어떻게 청구 내 변경 마이그레이션된 toohello 단일 파티션 컬렉션 난 후?</span><span class="sxs-lookup"><span data-stu-id="ca96f-171">How will my billing change after I’m migrated toohello single partition collections?</span></span>

<span data-ttu-id="ca96f-172">가정 하 고 10 S1 컬렉션, 1GB의 저장소에 대해 각각, hello 미국 동부 지역에 있고 400 RU/sec (hello 최소 수준)에서 이러한 10 S1 컬렉션 too10 단일 파티션 컬렉션을 마이그레이션하세요.</span><span class="sxs-lookup"><span data-stu-id="ca96f-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in hello US East region, and you migrate these 10 S1 collections too10 single partition collections at 400 RU/sec (hello minimum level).</span></span> <span data-ttu-id="ca96f-173">청구서 달에 대 한 hello 10 단일 파티션 컬렉션을 유지 하는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-173">Your bill will look as follows if you keep hello 10 single partition collections for a full month:</span></span>

![10 개의 컬렉션에 대 한 가격 책정 S1 too10 컬렉션을 비교 하는 방법을 단일 파티션 컬렉션에 대 한 가격을 사용 하 여](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="ca96f-175">저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="ca96f-176">데이터 tooa 사실상 사용 하 여 컬렉션을 분할 하는 hello Cosmos DB 데이터 마이그레이션 도구 toomigrate S1, S2 또는 S3 성능 수준에 따라 컬렉션 하는지 여부는 모두 10GB의 사용 가능한 저장 공간, 단일 파티션 컬렉션을 사용할 수 있습니다. 무제한 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use hello Cosmos DB Data Migration tool toomigrate your data tooa partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="ca96f-177">분할 된 컬렉션의 hello 이점에 대 한 정보를 참조 하십시오. [Partitioning 및 Azure Cosmos DB에 크기 조정](documentdb-partition-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-177">For information about hello benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="ca96f-178">방법에 대 한 내용은 toomigrate S1, S2, S3, 또는 단일 파티션 컬렉션 분할 tooa 컬렉션 참조 [toopartitioned 단일 파티션 컬렉션에서 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-178">For information about how toomigrate your S1, S2, S3, or single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="ca96f-179">2017 년 8 월 1 하기 전에 hello S1, S2, S3 성능 수준 간에 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ca96f-179">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="ca96f-180">기존 계정만 S1, S2, S3 성능 수 toochange 되며 hello 포털을 통해 또는 프로그래밍 방식으로 성능 수준의 계층을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-180">Only existing accounts with S1, S2, and S3 performance will be able toochange and alter performance level tiers through hello portal or programmatically.</span></span> <span data-ttu-id="ca96f-181">2017 년 8 월 1 하 여 S1, S2, hello 및 S3 성능 수준을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-181">By August 1, 2017, hello S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="ca96f-182">S1, S3, 또는 S3 tooa 단일 파티션 컬렉션에서 변경할 S1, S2 또는 S3 성능 수준 toohello 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-182">If you change from S1, S3, or S3 tooa single partition collection, you cannot return toohello S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="ca96f-183">내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="ca96f-184">hello 마이그레이션 2017 년 7 월 31에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-184">hello migration will occur on July 31, 2017.</span></span> <span data-ttu-id="ca96f-185">컬렉션 hello S1, S2를 사용 하 여 또는 S3 성능 수준 hello Cosmos DB 팀 연락을 드릴 전자 메일을 통해 hello 마이그레이션 수행 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-185">If you have a collection that uses hello S1, S2 or S3 performance levels, hello Cosmos DB team will contact you by email before hello migration takes place.</span></span> <span data-ttu-id="ca96f-186">2017 년 8 월 1에 hello 마이그레이션이 완료 되 면 Azure 포털 hello 컬렉션 표준 가격 책정을 사용 하도록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-186">Once hello migration is complete, on August 1, 2017, hello Azure portal will show that your collection uses Standard pricing.</span></span>

![어떻게 tooconfirm 사용자 컬렉션에 toohello 표준 가격 책정 계층 마이그레이션](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a><span data-ttu-id="ca96f-188">Hello S1, S2, S3 성능 수준 toosingle 파티션 컬렉션 직접에서 마이그레이션하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="ca96f-188">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>

<span data-ttu-id="ca96f-189">Hello S1, S2에서 마이그레이션할 수 있습니다 및 S3 성능 수준이 toosingle 파티션 컬렉션 hello Azure 포털을 사용 하 여 또는 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-189">You can migrate from hello S1, S2, and S3 performance levels toosingle partition collections using hello Azure portal or programmatically.</span></span> <span data-ttu-id="ca96f-190">단일 파티션 컬렉션으로 사용할 수 있는 hello 유연한 처리량 옵션 중에서 8 월 1 일 전에 직접 toobenefit에 이렇게 하려면 또는 2017 년 7 월 31에서 사용자 컬렉션을 마이그레이션할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-190">You can do this on your own before August 1 toobenefit from hello flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="ca96f-191">**hello Azure 포털을 사용 하 여 toomigrate toosingle 파티션 컬렉션**</span><span class="sxs-lookup"><span data-stu-id="ca96f-191">**toomigrate toosingle partition collections using hello Azure portal**</span></span>

1. <span data-ttu-id="ca96f-192">Hello에 [ **Azure 포털**](https://portal.azure.com), 클릭 **Azure Cosmos DB**, hello Cosmos DB 계정 toomodify를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-192">In hello [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select hello Cosmos DB account toomodify.</span></span> 
 
    <span data-ttu-id="ca96f-193">경우 **Azure Cosmos DB** Jumpbar hello를 클릭 하지는 >, 너무 스크롤하여**데이터베이스**을 선택 **Azure Cosmos DB**, 한 다음 hello DocumentDB 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-193">If **Azure Cosmos DB** is not on hello Jumpbar, click >, scroll too**Databases**, select **Azure Cosmos DB**, and then select hello DocumentDB account.</span></span>  

2. <span data-ttu-id="ca96f-194">Hello 리소스 메뉴에서 아래 **컨테이너**, 클릭 **배율**hello 컬렉션 toomodify hello 드롭 다운 목록에서 선택한 다음 클릭 **가격 책정 계층**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-194">On hello resource menu, under **Containers**, click **Scale**, select hello collection toomodify from hello drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="ca96f-195">미리 정의된 처리량을 사용하는 계정은 S1, S2 또는 S3의 가격 책정 계층을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="ca96f-196">Hello에 **가격 책정 계층을 선택** 블레이드에서 클릭 **표준** toochange toouser 정의 된 처리량을 클릭 하 고 **선택** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-196">In hello **Choose your pricing tier** blade, click **Standard** toochange toouser-defined throughput, and then click **Select** toosave your change.</span></span>

    ![여기서 toochange hello 처리량 값을 보여 주는 hello 설정 블레이드의 스크린샷](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="ca96f-198">Hello에 다시 **배율** 블레이드, hello **가격 책정 계층** 너무 변경**표준** 및 hello **처리량 (000RU/s)** 된 상자가 표시 됩니다는 400의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-198">Back in hello **Scale** blade, hello **Pricing Tier** is changed too**Standard** and hello **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="ca96f-199">400에서 10,000 사이 집합 hello 처리량 [요청 단위](request-units.md)-초당 (000RU/s).</span><span class="sxs-lookup"><span data-stu-id="ca96f-199">Set hello throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="ca96f-200">hello **예상 월별 요금 청구** hello hello 맨 아래에 페이지 자동으로 업데이트 tooprovide hello 월별 비용의 추정치입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-200">hello **Estimated Monthly Bill** at hello bottom of hello page updates automatically tooprovide an estimate of hello monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="ca96f-201">변경 내용을 저장 하 고 이동 toohello 표준 가격 책정 계층을 롤백할 수 없습니다 toohello S1, S2 또는 S3 성능 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-201">Once you save your changes and move toohello Standard pricing tier, you cannot roll back toohello S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="ca96f-202">클릭 **저장** toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-202">Click **Save** toosave your changes.</span></span>

    <span data-ttu-id="ca96f-203">더 많은 처리량(10,000RU/s 초과) 또는 더 많은 저장소(10GB 초과)가 필요하다고 판단되는 경우 분할된 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="ca96f-204">단일 파티션 컬렉션 분할 tooa 컬렉션 toomigrate 참조 [toopartitioned 단일 파티션 컬렉션에서 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-204">toomigrate a single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca96f-205">S1, S2 또는 S3 tooStandard에서 변경 too2 분을 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-205">Changing from S1, S2, or S3 tooStandard may take up too2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="ca96f-206">**hello.NET SDK를 사용 하 여 toomigrate toosingle 파티션 컬렉션**</span><span class="sxs-lookup"><span data-stu-id="ca96f-206">**toomigrate toosingle partition collections using hello .NET SDK**</span></span>

<span data-ttu-id="ca96f-207">컬렉션의 성능 수준 변경에 대한 다른 옵션은 SDK를 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="ca96f-208">이 섹션에만 컬렉션의 성능 변경 적용를 사용 하 여 수준 우리의 [DocumentDB.NET API](documentdb-sdk-dotnet.md), 하지만 hello 프로세스는 우리의 다른 Sdk에 대 한 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but hello process is similar for our other SDKs.</span></span>

<span data-ttu-id="ca96f-209">초당 요청 단위 000 hello 컬렉션 처리량 too5 변경에 대 한 코드 조각을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-209">Here is a code snippet for changing hello collection throughput too5,000 request units per second:</span></span>
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="ca96f-210">방문 [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview 추가 예제 및 우리의 제안 방법에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="ca96f-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="ca96f-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="ca96f-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="ca96f-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="ca96f-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="ca96f-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="ca96f-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="ca96f-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="ca96f-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="ca96f-215">EA 고객에게 미치는 영향은?</span><span class="sxs-lookup"><span data-stu-id="ca96f-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="ca96f-216">EA 고객은 자신의 현재 계약 hello 끝날 때까지 보호 가격 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-216">EA customers will be price protected until hello end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca96f-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca96f-217">Next steps</span></span>
<span data-ttu-id="ca96f-218">가격 및 관리 Azure Cosmos DB를 사용 하 여 데이터에 대해 자세히 toolearn이 리소스를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-218">toolearn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="ca96f-219">[Cosmos DB의 데이터 분할](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="ca96f-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="ca96f-220">분할 전략 tooscale를 원활 하 게 구현에 대 한 팁 뿐만 아니라 단일 파티션 컨테이너 및 분할 된 컨테이너의 hello 차이점을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-220">Understand hello difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy tooscale seamlessly.</span></span>
2.  <span data-ttu-id="ca96f-221">[Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ca96f-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="ca96f-222">처리량을 프로 비전 하 고 저장소 사용의 hello 비용에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-222">Learn about hello cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="ca96f-223">[요청 단위](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ca96f-223">[Request units](request-units.md).</span></span> <span data-ttu-id="ca96f-224">읽기, 쓰기, 쿼리 예를 들어, 다른 작업 형식에 대 한 처리량의 hello 사용량을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca96f-224">Understand hello consumption of throughput for different operation types, for example Read, Write, Query.</span></span>

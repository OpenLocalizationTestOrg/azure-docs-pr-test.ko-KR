---
title: "프리미엄 Azure Redis Cache에 데이터 지속성을 구성하는 방법"
description: "프리미엄 계층 Azure Redis Cache 인스턴스에 대해 데이터 지속성을 구성하고 관리하는 방법에 대해 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 638f0154d3a4fd091197a2da86374a053b31c4c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-persistence-for-a-premium-azure-redis-cache"></a><span data-ttu-id="78463-103">프리미엄 Azure Redis Cache에 데이터 지속성을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="78463-103">How to configure data persistence for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="78463-104">Azure Redis Cache에는 클러스터링, 지속성, 가상 네트워크 지원 등의 프리미엄 계층 기능을 포함하여 캐시 크기 및 기능을 유연하게 선택할 수 있는 다양한 캐시 제품이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-104">Azure Redis Cache has different cache offerings which provide flexibility in the choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="78463-105">이 문서에서는 프리미엄 Azure Redis Cache에서 지속성을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-105">This article describes how to configure persistence in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="78463-106">다른 프리미엄 캐시 기능에 대한 자세한 내용은 [Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78463-106">For information on other premium cache features, see [Introduction to the Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-data-persistence"></a><span data-ttu-id="78463-107">데이터 지속성이란?</span><span class="sxs-lookup"><span data-stu-id="78463-107">What is data persistence?</span></span>
<span data-ttu-id="78463-108">[Redis 지속성](https://redis.io/topics/persistence)을 사용하면 Redis에 저장된 데이터를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-108">[Redis persistence](https://redis.io/topics/persistence) allows you to persist data stored in Redis.</span></span> <span data-ttu-id="78463-109">또한 스냅숏을 만들고, 하드웨어 오류 시 로드할 수 있게 데이터를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-109">You can also take snapshots and back up the data, which you can load in case of a hardware failure.</span></span> <span data-ttu-id="78463-110">기본 또는 표준 계층보다 훨씬 큰 이러한 혜택은 모든 데이터가 메모리에 저장되기 때문에 가능하며 캐시 노드 다운 시 데이터 손실 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-110">This is a huge advantage over Basic or Standard tier where all the data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span></span> 

<span data-ttu-id="78463-111">Azure Redis Cache는 다음 모델을 사용하여 Redis 지속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-111">Azure Redis Cache offers Redis persistence using the following models:</span></span>

* <span data-ttu-id="78463-112">**RDB 지속성** - RDB(Redis 데이터베이스) 지속성이 구성된 경우 Azure Redis Cache는 구성 가능한 백업 주기에 따라 Redis 이진 형식으로 Redis cache의 스냅숏을 디스크에 지속적으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-112">**RDB persistence** - When RDB (Redis database) persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="78463-113">중대한 이벤트가 발생하여 주 및 복제본 캐시가 모두 비활성화된 경우 가장 최근의 스냅숏을 사용하여 캐시를 재구성합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-113">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the most recent snapshot.</span></span> <span data-ttu-id="78463-114">RDB 지속성의 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78463-114">Learn more about the [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="78463-115">**AOF 지속성** - AOF(파일만 연결) 지속성이 구성되면 Azure Redis Cache는 모든 쓰기 작업을 Azure Storage 계정에 초당 1번 이상 저장되는 로그에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-115">**AOF persistence** - When AOF (Append only file) persistence is configured, Azure Redis Cache saves every write operation to a log that is saved at least once per second into an Azure Storage account.</span></span> <span data-ttu-id="78463-116">중대한 이벤트가 발생하여 주 및 복제본 캐시가 모두 비활성화된 경우 저장된 쓰기 작업을 사용하여 캐시를 재구성합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-116">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the stored write operations.</span></span> <span data-ttu-id="78463-117">AOF 지속성의 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78463-117">Learn more about the [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="78463-118">지속성은 캐시를 만드는 동안 **새 Redis Cache** 블레이드에서 구성하거나 기존 프리미엄 캐시의 **리소스 메뉴**에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-118">Persistence is configured from the **New Redis Cache** blade during cache creation and on the **Resource menu** for existing premium caches.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="78463-119">프리미엄 가격 책정 계층을 선택한 다음 **Redis 지속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-119">Once a premium pricing tier is selected, click **Redis persistence**.</span></span>

![Redis 지속성][redis-cache-persistence]

<span data-ttu-id="78463-121">다음 섹션의 단계에서는 새 프리미엄 캐시에서 Redis 지속성을 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-121">The steps in the next section describe how to configure Redis persistence on your new premium cache.</span></span> <span data-ttu-id="78463-122">Redis 지속성이 구성되어 있는 경우 **만들기** 를 클릭하여 Redis 지속성을 사용하는 새 프리미엄 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78463-122">Once Redis persistence is configured, click **Create** to create your new premium cache with Redis persistence.</span></span>

## <a name="enable-redis-persistence"></a><span data-ttu-id="78463-123">Redis 지속성 사용</span><span class="sxs-lookup"><span data-stu-id="78463-123">Enable Redis persistence</span></span>

<span data-ttu-id="78463-124">Redis 지속성은 **Redis 데이터 지속성** 블레이드에서 **RDB** 또는 **AOF** 지속성을 선택하여 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-124">Redis persistence is enabled on the **Redis data persistence** blade by choosing either **RDB** or **AOF** persistence.</span></span> <span data-ttu-id="78463-125">새 캐시의 경우 위의 섹션에서 설명한 대로 캐시 만들기 프로세스 중 이 블레이드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-125">For new caches, this blade is accessed during the cache creation process, as described in the previous section.</span></span> <span data-ttu-id="78463-126">기존 캐시의 경우 캐시의 **리소스 메뉴** 블레이드에서 **Redis 데이터 지속성** 블레이드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-126">For existing caches, the **Redis data persistence** blade is accessed from the **Resource menu** for your cache.</span></span>

![Redis 설정][redis-cache-settings]


## <a name="configure-rdb-persistence"></a><span data-ttu-id="78463-128">RDB 지속성 구성</span><span class="sxs-lookup"><span data-stu-id="78463-128">Configure RDB persistence</span></span>

<span data-ttu-id="78463-129">RDB 지속성을 사용하도록 설정하려면 **RDB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-129">To enable RDB persistence, click **RDB**.</span></span> <span data-ttu-id="78463-130">이전에 사용하도록 설정한 프리미엄 캐시에서 Redis 지속성을 사용하지 않도록 설정하려면 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-130">To disable RDB persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis RDB 지속성][redis-cache-rdb-persistence]

<span data-ttu-id="78463-132">백업 간격을 구성하려면 드롭다운 목록에서 **백업 빈도** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-132">To configure the backup interval, select a **Backup Frequency** from the drop-down list.</span></span> <span data-ttu-id="78463-133">**15분**, **30분**, **60분**, **6시간**, **12시간** 및 **24시간** 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-133">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span></span> <span data-ttu-id="78463-134">이 간격은 이전 백업 작업이 성공적으로 완료되어 새 백업이 시작된 시점부터 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-134">This interval starts counting down after the previous backup operation successfully completes and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="78463-135">**저장소 계정**을 클릭하여 사용할 저장소 계정을 선택하고 **저장소 키** 드롭다운 목록에서 사용할 **기본 키** 또는 **보조 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-135">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> <span data-ttu-id="78463-136">캐시와 동일한 영역에 있는 저장소 계정을 선택해야 하며 높은 처리량을 가진 **프리미엄 저장소** 계정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-136">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="78463-137">지속성 계정에 대한 저장소 키가 다시 생성된 경우에는 **저장소 키** 드롭다운에서 원하는 키를 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-137">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="78463-138">**확인** 을 클릭하여 지속성 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-138">Click **OK** to save the persistence configuration.</span></span>

<span data-ttu-id="78463-139">백업 빈도 간격이 경과되면 다음 백업(새 캐시의 경우 첫 번째 백업)이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-139">The next backup (or first backup for new caches) is initiated once the backup frequency interval elapses.</span></span>

## <a name="configure-aof-persistence"></a><span data-ttu-id="78463-140">AOF 지속성 구성</span><span class="sxs-lookup"><span data-stu-id="78463-140">Configure AOF persistence</span></span>

<span data-ttu-id="78463-141">AOF 지속성을 사용하도록 설정하려면 **AOF**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-141">To enable AOF persistence, click **AOF**.</span></span> <span data-ttu-id="78463-142">이전에 사용하도록 설정한 프리미엄 캐시에서 AOF 지속성을 사용하지 않도록 설정하려면 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-142">To disable AOF persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis AOF 지속성][redis-cache-aof-persistence]

<span data-ttu-id="78463-144">AOF 지속성을 구성하려면 **첫 저장소 계정**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-144">To configure AOF persistence, specify a **First Storage Account**.</span></span> <span data-ttu-id="78463-145">이 저장소 계정은 캐시와 동일한 영역에 있어야 하며 높은 처리량을 가진 **프리미엄 저장소** 계정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-145">This storage account must be in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> <span data-ttu-id="78463-146">경우에 따라 **두 번째 저장소 계정**이라는 추가 저장소 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-146">You can optionally configure an additional storage account named **Second Storage Account**.</span></span> <span data-ttu-id="78463-147">두 번째 저장소 계정이 구성된 경우 복제본 캐시에 대한 쓰기는 이 두 번째 저장소 계정에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-147">If a second storage account is configured, the writes to the replica cache are written to this second storage account.</span></span> <span data-ttu-id="78463-148">구성된 각 저장소 계정에 대해 **저장소 키** 드롭다운에서 사용할 **기본 키** 또는 **보조 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-148">For each configured storage account, choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="78463-149">지속성 계정에 대한 저장소 키가 다시 생성된 경우에는 **저장소 키** 드롭다운에서 원하는 키를 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-149">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="78463-150">AOF 지속성을 사용하도록 설정하면 캐시에 대한 쓰기 작업이 지정된 저장소 계정(두 번째 저장소 계정을 구성한 경우 해당 계정도 포함)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-150">When AOF persistence is enabled, write operations to the cache are saved to the designated storage account (or accounts if you have configured a second storage account).</span></span> <span data-ttu-id="78463-151">주 캐시와 복제본 캐시 둘 다에서 심각한 오류가 발생하면 저장된 AOF 로그가 캐시를 다시 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-151">In the event of a catastrophic failure that takes down both the primary and replica cache, the stored AOF log is used to rebuild the cache.</span></span>

## <a name="persistence-faq"></a><span data-ttu-id="78463-152">지속성 FAQ</span><span class="sxs-lookup"><span data-stu-id="78463-152">Persistence FAQ</span></span>
<span data-ttu-id="78463-153">다음 목록에는 Azure Redis Cache 지속성에 대해 일반적으로 묻는 질문과 답변이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-153">The following list contains answers to commonly asked questions about Azure Redis Cache persistence.</span></span>

* [<span data-ttu-id="78463-154">이전에 만든 캐시에서 지속성을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-154">Can I enable persistence on a previously created cache?</span></span>](#can-i-enable-persistence-on-a-previously-created-cache)
* [<span data-ttu-id="78463-155">AOF 및 RDB 지속성을 동시에 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-155">Can I enable AOF and RDB persistence at the same time?</span></span>](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [<span data-ttu-id="78463-156">어떤 지속성 모델을 선택해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="78463-156">Which persistence model should I choose?</span></span>](#which-persistence-model-should-i-choose)
* [<span data-ttu-id="78463-157">다른 크기로 확장했고 크기 조정 작업 전에 만들어진 백업을 복원할 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="78463-157">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a><span data-ttu-id="78463-158">RDB 지속성</span><span class="sxs-lookup"><span data-stu-id="78463-158">RDB persistence</span></span>
* [<span data-ttu-id="78463-159">캐시를 만든 후 RDB 백업 주기를 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-159">Can I change the RDB backup frequency after I create the cache?</span></span>](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [<span data-ttu-id="78463-160">RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-160">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [<span data-ttu-id="78463-161">새 백업을 만들면 이전 RDB 백업은 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-161">What happens to the old RDB backups when a new backup is made?</span></span>](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a><span data-ttu-id="78463-162">AOF 지속성</span><span class="sxs-lookup"><span data-stu-id="78463-162">AOF persistence</span></span>
* [<span data-ttu-id="78463-163">두 번째 저장소 계정은 언제 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="78463-163">When should I use a second storage account?</span></span>](#when-should-i-use-a-second-storage-account)
* [<span data-ttu-id="78463-164">AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="78463-164">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [<span data-ttu-id="78463-165">두 번째 저장소 계정은 어떻게 제거할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-165">How can I remove the second storage account?</span></span>](#how-can-i-remove-the-second-storage-account)
* [<span data-ttu-id="78463-166">다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="78463-166">What is a rewrite and how does it affect my cache?</span></span>](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [<span data-ttu-id="78463-167">AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-167">What should I expect when scaling a cache with AOF enabled?</span></span>](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [<span data-ttu-id="78463-168">저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-168">How is my AOF data organized in storage?</span></span>](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a><span data-ttu-id="78463-169">이전에 만든 캐시에서 지속성을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-169">Can I enable persistence on a previously created cache?</span></span>
<span data-ttu-id="78463-170">예, Redis 지속성은 캐시를 만들 때와 기존 프리미엄 캐시에서 모두 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-170">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span></span>

### <a name="can-i-enable-aof-and-rdb-persistence-at-the-same-time"></a><span data-ttu-id="78463-171">AOF 및 RDB 지속성을 동시에 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-171">Can I enable AOF and RDB persistence at the same time?</span></span>

<span data-ttu-id="78463-172">아니요. RDB 또는 AOF 중 하나만 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-172">No, you can enable only RDB or AOF, but not both at the same time.</span></span>

### <a name="which-persistence-model-should-i-choose"></a><span data-ttu-id="78463-173">어떤 지속성 모델을 선택해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="78463-173">Which persistence model should I choose?</span></span>

<span data-ttu-id="78463-174">AOF 지속성은 모든 쓰기를 로그에 저장하므로, 구성된 백업 간격을 기준으로 백업을 저장하여 성능에 최소 영향을 미치는 RDB 지속성과 비교할 때 처리량에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-174">AOF persistence saves every write to a log, which has some impact on throughput, compared with RDB persistence which saves backups based on the configured backup interval, with minimal impact on performance.</span></span> <span data-ttu-id="78463-175">기본 목표가 데이터 손실을 최소화하는 것이며 캐시에 대한 처리량 감소를 처리할 수 있는 경우에는 AOF 지속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-175">Choose AOF persistence if your primary goal is to minimize data loss, and you can handle a decrease in throughput for your cache.</span></span> <span data-ttu-id="78463-176">캐시에 대해 최적의 처리량을 유지하려고 하면서도 데이터 복구 메커니즘을 계속 유지하려는 경우에는 RDB 지속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-176">Choose RDB persistence if you wish to maintain optimal throughput on your cache, but still want a mechanism for data recovery.</span></span>

* <span data-ttu-id="78463-177">RDB 지속성의 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78463-177">Learn more about the [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="78463-178">AOF 지속성의 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78463-178">Learn more about the [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="78463-179">AOF 지속성을 사용하는 경우 성능에 대한 자세한 내용은 [AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78463-179">For more information on performance when using AOF persistence, see [Does AOF persistence affect throughout, latency, or performance of my cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span></span>

### <a name="what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation"></a><span data-ttu-id="78463-180">다른 크기로 확장했고 크기 조정 작업 전에 만들어진 백업을 복원할 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="78463-180">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>

<span data-ttu-id="78463-181">RDB 및 AOF 지속성:</span><span class="sxs-lookup"><span data-stu-id="78463-181">For both RDB and AOF persistence:</span></span>

* <span data-ttu-id="78463-182">더 큰 크기로 조정했다면 영향은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-182">If you have scaled to a larger size, there is no impact.</span></span>
* <span data-ttu-id="78463-183">더 작은 크기를 조정했고 새 크기에 대한 [데이터베이스 제한](cache-configure.md#databases)보다 사용자 지정 [데이터베이스](cache-configure.md#databases) 설정이 더 크다면, 그러한 데이터베이스에 저장된 데이터는 복원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-183">If you have scaled to a smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than the [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't restored.</span></span> <span data-ttu-id="78463-184">자세한 내용은 [사용자 지정 데이터베이스 설정이 크기 조정 동안 영향을 받나요?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span><span class="sxs-lookup"><span data-stu-id="78463-184">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span></span>
* <span data-ttu-id="78463-185">더 작은 크기로 조정 했고 마지막 백업의 모든 데이터를 저장하기에 충분한 공간이 더 작은 크기에 없는 경우, 일반적으로 [allkeys-lru](http://redis.io/topics/lru-cache) 제거 정책을 사용하여 복원 프로세스 중에 키가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-185">If you have scaled to a smaller size, and there isn't enough room in the smaller size to hold all of the data from the last backup, keys will be evicted during the restore process, typically using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span>

### <a name="can-i-change-the-rdb-backup-frequency-after-i-create-the-cache"></a><span data-ttu-id="78463-186">캐시를 만든 후 RDB 백업 주기를 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-186">Can I change the RDB backup frequency after I create the cache?</span></span>
<span data-ttu-id="78463-187">그렇습니다. **Redis 데이터 지속성** 블레이드에서 RDB 지속성에 대한 백업 빈도를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-187">Yes, you can change the backup frequency for RDB persistence on the **Redis data persistence** blade.</span></span> <span data-ttu-id="78463-188">자세한 내용은 [Redis 지속성 구성](#configure-redis-persistence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78463-188">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span></span>

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a><span data-ttu-id="78463-189">RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-189">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>
<span data-ttu-id="78463-190">RDB 지속성 백업 간격의 주기는 이전 백업 프로세스가 성공적으로 완료되어야 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-190">The RDB persistence backup frequency interval does not start until the previous backup process has completed successfully.</span></span> <span data-ttu-id="78463-191">백업 간격이 60분이고 백업 프로세스를 성공적으로 완료하는 데 15분이 걸린다면 다음 백업은 이전 백업 시작 시점에서 75분까지 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-191">If the backup frequency is 60 minutes and it takes a backup process 15 minutes to successfully complete, the next backup won't start until 75 minutes after the start time of the previous backup.</span></span>

### <a name="what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made"></a><span data-ttu-id="78463-192">새 백업을 만들면 이전 RDB 백업은 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-192">What happens to the old RDB backups when a new backup is made?</span></span>
<span data-ttu-id="78463-193">가장 최근 백업을 제외한 모든 RDB 지속성 백업은 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-193">All RDB persistence backups except for the most recent one are automatically deleted.</span></span> <span data-ttu-id="78463-194">즉시 삭제되지 않을 수 있으나 오래된 백업을 무한정 유지하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-194">This deletion may not happen immediately but older backups are not persisted indefinitely.</span></span>


### <a name="when-should-i-use-a-second-storage-account"></a><span data-ttu-id="78463-195">두 번째 저장소 계정은 언제 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="78463-195">When should I use a second storage account?</span></span>

<span data-ttu-id="78463-196">AOF 지속성이 캐시에 대해 예상된 설정 작업보다 더 높다고 판단되면 AOF 지속성에 대해 두 번째 저장소 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-196">You should use a second storage account for AOF persistence when you believe you have higher than expected set operations on the cache.</span></span>  <span data-ttu-id="78463-197">보조 저장소 계정을 설정하면 캐시가 저장소 대역폭 제한에 도달하지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-197">Setting up the secondary storage account helps ensure your cache doesn't reach storage bandwidth limits.</span></span>

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a><span data-ttu-id="78463-198">AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="78463-198">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>

<span data-ttu-id="78463-199">AOF 지속성은 캐시가 최대 부하보다 낮을 때(CPU 및 서버 부하 둘 다에서 90% 미만) 처리량에 15%-20% 정도 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-199">AOF persistence affects throughput by about 15% – 20% when the cache is below maximum load (CPU and Server Load both under 90%).</span></span> <span data-ttu-id="78463-200">캐시가 이러한 한도 내에 있을 때 대기 시간 문제는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-200">There should not be latency issues when the cache is within these limits.</span></span> <span data-ttu-id="78463-201">그러나 캐시는 AOF가 사용하도록 설정되면 더 빨리 이러한 한도에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-201">However, the cache will reach these limits sooner with AOF enabled.</span></span>

### <a name="how-can-i-remove-the-second-storage-account"></a><span data-ttu-id="78463-202">두 번째 저장소 계정은 어떻게 제거할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="78463-202">How can I remove the second storage account?</span></span>

<span data-ttu-id="78463-203">두 번째 저장소 계정을 첫 번째 저장소 계정과 동일하게 설정하여 AOF 지속성 보조 저장소 계정을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-203">You can remove the AOF persistence secondary storage account by setting the second storage account to be the same as the first storage account.</span></span> <span data-ttu-id="78463-204">자세한 내용은 [AOF 지속성 구성](#configure-aof-persistence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78463-204">For instructions, see [Configure AOF persistence](#configure-aof-persistence).</span></span>

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a><span data-ttu-id="78463-205">다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="78463-205">What is a rewrite and how does it affect my cache?</span></span>

<span data-ttu-id="78463-206">AOF 파일이 충분히 커지면 다시 쓰기가 자동으로 큐에 대기됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-206">When the AOF file becomes large enough, a rewrite is automatically queued on the cache.</span></span> <span data-ttu-id="78463-207">다시 쓰기를 수행하면 현재 데이터 집합을 만드는 데 필요한 작업의 최소 집합을 사용하여 AOF 파일 크기가 다시 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-207">The rewrite resizes the AOF file with the minimal set of operations needed to create the current data set.</span></span> <span data-ttu-id="78463-208">다시 쓰기 동안, 성능 제한에 더 빠르게 도달하며 큰 데이터 집합을 처리할 때 특히 더 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-208">During rewrites, expect to reach performance limits sooner especially when dealing with large datasets.</span></span> <span data-ttu-id="78463-209">AOF 파일이 더 커지면 다시 쓰기는 덜 자주 발생하지만 일단 발생하면 많은 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-209">Rewrites occur less often as the AOF file becomes larger, but will take a significant amount of time when it happens.</span></span>

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a><span data-ttu-id="78463-210">AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-210">What should I expect when scaling a cache with AOF enabled?</span></span>

<span data-ttu-id="78463-211">크기 조정이 완료된 후에 파일이 다시 로드되므로 크기 조정 시 AOF 파일이 아주 커질 경우 크기 조정 작업이 예상한 것보다 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="78463-211">If the AOF file at the time of scaling is significantly large, then expect the scale operation to take longer than expected since it will be reloading the file after scaling has finished.</span></span>

<span data-ttu-id="78463-212">크기 조정에 대한 자세한 내용은 [다른 크기로 확장했고 크기 조정 작업 전에 만들어진 백업을 복원할 경우 어떻게 됩니까?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78463-212">For more information on scaling, see [What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span></span>

### <a name="how-is-my-aof-data-organized-in-storage"></a><span data-ttu-id="78463-213">저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?</span><span class="sxs-lookup"><span data-stu-id="78463-213">How is my AOF data organized in storage?</span></span>

<span data-ttu-id="78463-214">AOF 파일에 저장된 데이터는 저장소에 데이터를 저장하는 성능을 향상시키기 위해 노드당 여러 페이지 Blob으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-214">Data stored in AOF files is divided into multiple page blobs per node to increase performance of saving the data to storage.</span></span> <span data-ttu-id="78463-215">다음 표에는 각 가격 책정 계층에 사용되는 페이지 Blob 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-215">The following table displays how many page blobs are used for each pricing tier:</span></span>

| <span data-ttu-id="78463-216">프리미엄 계층</span><span class="sxs-lookup"><span data-stu-id="78463-216">Premium tier</span></span> | <span data-ttu-id="78463-217">Blob</span><span class="sxs-lookup"><span data-stu-id="78463-217">Blobs</span></span> |
|--------------|-------|
| <span data-ttu-id="78463-218">P1</span><span class="sxs-lookup"><span data-stu-id="78463-218">P1</span></span>           | <span data-ttu-id="78463-219">분할당 4</span><span class="sxs-lookup"><span data-stu-id="78463-219">4 per shard</span></span>    |
| <span data-ttu-id="78463-220">P2</span><span class="sxs-lookup"><span data-stu-id="78463-220">P2</span></span>           | <span data-ttu-id="78463-221">분할당 8</span><span class="sxs-lookup"><span data-stu-id="78463-221">8 per shard</span></span>    |
| <span data-ttu-id="78463-222">P3</span><span class="sxs-lookup"><span data-stu-id="78463-222">P3</span></span>           | <span data-ttu-id="78463-223">분할당 16</span><span class="sxs-lookup"><span data-stu-id="78463-223">16 per shard</span></span>   |
| <span data-ttu-id="78463-224">P4</span><span class="sxs-lookup"><span data-stu-id="78463-224">P4</span></span>           | <span data-ttu-id="78463-225">분할당 20</span><span class="sxs-lookup"><span data-stu-id="78463-225">20 per shard</span></span>   |

<span data-ttu-id="78463-226">클러스터링을 사용하도록 설정하면 캐시의 각 분할은 이전 표에 표시된 것처럼 자체 페이지 Blob 집합을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="78463-226">When clustering is enabled, each shard in the cache has its own set of page blobs, as indicated in the previous table.</span></span> <span data-ttu-id="78463-227">예를 들어 분할이 3개 있는 P2 캐시는 24개 페이지 Blob에 해당 AOF 파일을 분산합니다(분할당 8 Blob, 3개 분할).</span><span class="sxs-lookup"><span data-stu-id="78463-227">For example, a P2 cache with three shards distributes its AOF file across 24 page blobs (8 blobs per shard, with 3 shards).</span></span>

<span data-ttu-id="78463-228">다시 쓰기 후 2개의 AOF 파일 집합이 저장소에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="78463-228">After a rewrite, two sets of AOF files exist in storage.</span></span> <span data-ttu-id="78463-229">다시 쓰기는 백그라운드에서 발생하며 첫 번째 파일 집합에 추가되지만, 다시 쓰기 동안 캐시로 전송된 설정 작업은 두 번째 집합에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-229">Rewrites occur in the background and append to the first set of files, while set operations that are sent to the cache during the rewrite append to the second set.</span></span> <span data-ttu-id="78463-230">오류가 발생한 경우 백업은 다시 쓰기 동안 일시적으로 저장되지만 다시 쓰기가 끝난 후에 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="78463-230">A backup is temporarily stored during rewrites in case of failure, but is promptly deleted after a rewrite finishes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78463-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78463-231">Next steps</span></span>
<span data-ttu-id="78463-232">더 많은 프리미엄 캐시 기능을 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78463-232">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="78463-233">Azure Redis Cache 프리미엄 계층 소개</span><span class="sxs-lookup"><span data-stu-id="78463-233">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png

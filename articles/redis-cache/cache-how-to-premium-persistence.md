---
title: "프리미엄 Azure Redis Cache에 대 한 aaaHow tooconfigure 데이터 지 속성"
description: "자세한 내용은 방법 tooconfigure 및 프리미엄 계층 Azure Redis 캐시 인스턴스 데이터 유지 관리"
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
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a><span data-ttu-id="2017b-103">어떻게 Premium Azure Redis Cache에 대 한 tooconfigure 데이터 지 속성</span><span class="sxs-lookup"><span data-stu-id="2017b-103">How tooconfigure data persistence for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="2017b-104">Azure Redis 캐시 캐시 크기 및 기능, 프리미엄 계층 기능 클러스터링, 지 속성 및 가상 네트워크 지원 등을 포함 하 여 hello 선택에서 유연성을 제공 하는 다른 캐시 기능에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-104">Azure Redis Cache has different cache offerings which provide flexibility in hello choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="2017b-105">이 문서에서는 Azure Redis 캐시 하는 한 premium에서 tooconfigure 지 속성 방법 설명 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2017b-105">This article describes how tooconfigure persistence in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="2017b-106">다른 프리미엄 캐시 기능에 대 한 자세한 내용은 참조 [toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-106">For information on other premium cache features, see [Introduction toohello Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-data-persistence"></a><span data-ttu-id="2017b-107">데이터 지속성이란?</span><span class="sxs-lookup"><span data-stu-id="2017b-107">What is data persistence?</span></span>
<span data-ttu-id="2017b-108">[지 속성 redis](https://redis.io/topics/persistence) Redis에 저장 된 toopersist 데이터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-108">[Redis persistence](https://redis.io/topics/persistence) allows you toopersist data stored in Redis.</span></span> <span data-ttu-id="2017b-109">스냅숏을 하 고 하드웨어 오류가 발생할 경우 로드할 수 있는 hello 데이터를 백업할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-109">You can also take snapshots and back up hello data, which you can load in case of a hardware failure.</span></span> <span data-ttu-id="2017b-110">이것은 Basic의 이점을 활용 또는 표준 계층 데이터를 hello 모든 메모리에 저장 됩니다 및 다운은 캐시 노드가 되는 경우 오류가 발생 한 경우 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-110">This is a huge advantage over Basic or Standard tier where all hello data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span></span> 

<span data-ttu-id="2017b-111">Azure Redis 캐시는 모델을 따르는 hello를 사용 하 여 Redis 지 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-111">Azure Redis Cache offers Redis persistence using hello following models:</span></span>

* <span data-ttu-id="2017b-112">**RDB 지 속성** -때 RDB (Redis 데이터베이스)의 지 속성 구성, Azure Redis Cache hello Redis 캐시 구성 가능한 백업 빈도에 따라 이진 형식 toodisk Redis에 대 한 스냅숏을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-112">**RDB persistence** - When RDB (Redis database) persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="2017b-113">재해 발생 기본 hello와 복제본 캐시 모두 비활성화 하는 hello 캐시 hello 최신 스냅숏을 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-113">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache is reconstructed using hello most recent snapshot.</span></span> <span data-ttu-id="2017b-114">Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages) RDB 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-114">Learn more about hello [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="2017b-115">**지 속성 AOF** -때 AOF (Append 유일한 파일)의 지 속성 구성, Azure Redis Cache는 Azure 저장소 계정에는 초 당 최소 한 번 저장 되는 모든 쓰기 작업 tooa 로그를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-115">**AOF persistence** - When AOF (Append only file) persistence is configured, Azure Redis Cache saves every write operation tooa log that is saved at least once per second into an Azure Storage account.</span></span> <span data-ttu-id="2017b-116">재해 발생 기본 hello와 복제본 캐시 모두 비활성화 하는 hello 캐시 쓰기 작업을 저장 하는 hello를 사용 하 여 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-116">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache is reconstructed using hello stored write operations.</span></span> <span data-ttu-id="2017b-117">Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages) AOF 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-117">Learn more about hello [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="2017b-118">지 속성 hello에서 구성 된 **새 Redis 캐시** 블레이드 hello 및 캐시 만들기 중 **리소스 메뉴** 기존 프리미엄 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-118">Persistence is configured from hello **New Redis Cache** blade during cache creation and on hello **Resource menu** for existing premium caches.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="2017b-119">프리미엄 가격 책정 계층을 선택한 다음 **Redis 지속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-119">Once a premium pricing tier is selected, click **Redis persistence**.</span></span>

![Redis 지속성][redis-cache-persistence]

<span data-ttu-id="2017b-121">hello hello 다음 섹션의 단계에 설명 방법을 tooconfigure 새 프리미엄 캐시에 Redis 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-121">hello steps in hello next section describe how tooconfigure Redis persistence on your new premium cache.</span></span> <span data-ttu-id="2017b-122">Redis 지 속성 구성 되 면 클릭 **만들기** toocreate Redis 지 속성을 사용 하 여 새 프로그램 프리미엄 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-122">Once Redis persistence is configured, click **Create** toocreate your new premium cache with Redis persistence.</span></span>

## <a name="enable-redis-persistence"></a><span data-ttu-id="2017b-123">Redis 지속성 사용</span><span class="sxs-lookup"><span data-stu-id="2017b-123">Enable Redis persistence</span></span>

<span data-ttu-id="2017b-124">Redis hello에서 지 속성을 사용 하는 **Redis 데이터 지 속성** 블레이드 중 하나를 선택 하 여 **RDB** 또는 **AOF** 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-124">Redis persistence is enabled on hello **Redis data persistence** blade by choosing either **RDB** or **AOF** persistence.</span></span> <span data-ttu-id="2017b-125">새 캐시의 경우이 블레이드는 hello 이전 섹션에 설명 된 대로 hello 캐시를 만드는 프로세스 동안 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-125">For new caches, this blade is accessed during hello cache creation process, as described in hello previous section.</span></span> <span data-ttu-id="2017b-126">기존 캐시에 대 한 hello **Redis 데이터 지 속성** 블레이드 hello에서 액세스 **리소스 메뉴** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-126">For existing caches, hello **Redis data persistence** blade is accessed from hello **Resource menu** for your cache.</span></span>

![Redis 설정][redis-cache-settings]


## <a name="configure-rdb-persistence"></a><span data-ttu-id="2017b-128">RDB 지속성 구성</span><span class="sxs-lookup"><span data-stu-id="2017b-128">Configure RDB persistence</span></span>

<span data-ttu-id="2017b-129">tooenable RDB 지 속성 클릭 **RDB**합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-129">tooenable RDB persistence, click **RDB**.</span></span> <span data-ttu-id="2017b-130">이전에 설정 된 프리미엄 캐시에서 toodisable RDB 지 속성과 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-130">toodisable RDB persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis RDB 지속성][redis-cache-rdb-persistence]

<span data-ttu-id="2017b-132">tooconfigure hello 백업 간격을 선택는 **백업 빈도** hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-132">tooconfigure hello backup interval, select a **Backup Frequency** from hello drop-down list.</span></span> <span data-ttu-id="2017b-133">**15분**, **30분**, **60분**, **6시간**, **12시간** 및 **24시간** 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-133">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span></span> <span data-ttu-id="2017b-134">이 간격은 hello 이전 백업 작업이 성공적으로 완료 되 고이 경과 하면 새 백업을 시작 후 카운트다운을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-134">This interval starts counting down after hello previous backup operation successfully completes and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="2017b-135">클릭 **저장소 계정** tooselect 저장소 계정 toouse hello 선택한 어느 hello **기본 키** 또는 **보조 키** hello에서 toouse **저장소 키** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-135">Click **Storage Account** tooselect hello storage account toouse, and choose either hello **Primary key** or **Secondary key** toouse from hello **Storage Key** drop-down.</span></span> <span data-ttu-id="2017b-136">Hello에 저장소 계정을 선택 해야 hello 캐시와 동일한 지역 및 **프리미엄 저장소** 프리미엄 저장소 처리량이 높은 때문에 계정을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-136">You must choose a storage account in hello same region as hello cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2017b-137">Hello hello에서 원하는 키를 다시 구성 해야 지 속성 계정에 대 한 hello 저장소 키를 다시 생성 하는 경우 **저장소 키** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-137">If hello storage key for your persistence account is regenerated, you must reconfigure hello desired key from hello **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="2017b-138">클릭 **확인** toosave hello 지 속성 구성.</span><span class="sxs-lookup"><span data-stu-id="2017b-138">Click **OK** toosave hello persistence configuration.</span></span>

<span data-ttu-id="2017b-139">hello 백업 빈도 간격에 경과 되 면 hello (또는 새 캐시에 대 한 첫 번째 백업은 다음 백업)가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-139">hello next backup (or first backup for new caches) is initiated once hello backup frequency interval elapses.</span></span>

## <a name="configure-aof-persistence"></a><span data-ttu-id="2017b-140">AOF 지속성 구성</span><span class="sxs-lookup"><span data-stu-id="2017b-140">Configure AOF persistence</span></span>

<span data-ttu-id="2017b-141">tooenable AOF 지 속성 클릭 **AOF**합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-141">tooenable AOF persistence, click **AOF**.</span></span> <span data-ttu-id="2017b-142">이전에 설정 된 프리미엄 캐시에서 toodisable AOF 지 속성과 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-142">toodisable AOF persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis AOF 지속성][redis-cache-aof-persistence]

<span data-ttu-id="2017b-144">tooconfigure AOF 지 속성을 지정 된 **첫 저장소 계정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-144">tooconfigure AOF persistence, specify a **First Storage Account**.</span></span> <span data-ttu-id="2017b-145">이 저장소 계정은 hello에 있어야 hello 캐시와 동일한 지역 및 **프리미엄 저장소** 프리미엄 저장소 처리량이 높은 때문에 계정을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-145">This storage account must be in hello same region as hello cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> <span data-ttu-id="2017b-146">경우에 따라 **두 번째 저장소 계정**이라는 추가 저장소 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-146">You can optionally configure an additional storage account named **Second Storage Account**.</span></span> <span data-ttu-id="2017b-147">두 번째 저장소 계정이 구성 된 경우 hello 쓰기 toohello 복제본 캐시가 쓰여집니다 toothis 두 번째 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="2017b-147">If a second storage account is configured, hello writes toohello replica cache are written toothis second storage account.</span></span> <span data-ttu-id="2017b-148">각 구성 된 저장소 계정에 대해 선택 하거나 hello **기본 키** 또는 **보조 키** hello에서 toouse **저장소 키** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-148">For each configured storage account, choose either hello **Primary key** or **Secondary key** toouse from hello **Storage Key** drop-down.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2017b-149">Hello hello에서 원하는 키를 다시 구성 해야 지 속성 계정에 대 한 hello 저장소 키를 다시 생성 하는 경우 **저장소 키** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-149">If hello storage key for your persistence account is regenerated, you must reconfigure hello desired key from hello **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="2017b-150">AOF 지 속성을 사용 하는 경우 작업 toohello 캐시 toohello 저장소 계정 또는 계정을 두 번째 저장소 계정을 구성 하는 경우 지정 된 저장 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-150">When AOF persistence is enabled, write operations toohello cache are saved toohello designated storage account (or accounts if you have configured a second storage account).</span></span> <span data-ttu-id="2017b-151">치명적인 오류의 hello 이벤트에서 모두 다운은 hello 기본 및 복제본 캐시 hello 저장된 AOF 로그는 toorebuild hello 캐시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-151">In hello event of a catastrophic failure that takes down both hello primary and replica cache, hello stored AOF log is used toorebuild hello cache.</span></span>

## <a name="persistence-faq"></a><span data-ttu-id="2017b-152">지속성 FAQ</span><span class="sxs-lookup"><span data-stu-id="2017b-152">Persistence FAQ</span></span>
<span data-ttu-id="2017b-153">hello 다음 목록에 포함 되어 Azure Redis Cache 지 속성에 대 한 질문과 대답 toocommonly 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-153">hello following list contains answers toocommonly asked questions about Azure Redis Cache persistence.</span></span>

* [<span data-ttu-id="2017b-154">이전에 만든 캐시에서 지속성을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-154">Can I enable persistence on a previously created cache?</span></span>](#can-i-enable-persistence-on-a-previously-created-cache)
* [<span data-ttu-id="2017b-155">사용할 수 있습니까 hello에서 AOF 및 RDB 지 속성 동시?</span><span class="sxs-lookup"><span data-stu-id="2017b-155">Can I enable AOF and RDB persistence at hello same time?</span></span>](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [<span data-ttu-id="2017b-156">어떤 지속성 모델을 선택해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-156">Which persistence model should I choose?</span></span>](#which-persistence-model-should-i-choose)
* [<span data-ttu-id="2017b-157">Tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="2017b-157">What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?</span></span>](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a><span data-ttu-id="2017b-158">RDB 지속성</span><span class="sxs-lookup"><span data-stu-id="2017b-158">RDB persistence</span></span>
* [<span data-ttu-id="2017b-159">Hello 캐시를 만든 후 hello RDB 백업 빈도 변경 합니까?</span><span class="sxs-lookup"><span data-stu-id="2017b-159">Can I change hello RDB backup frequency after I create hello cache?</span></span>](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [<span data-ttu-id="2017b-160">RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-160">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [<span data-ttu-id="2017b-161">새 백업을 만들어질 때 toohello 오래 RDB 백업 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-161">What happens toohello old RDB backups when a new backup is made?</span></span>](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a><span data-ttu-id="2017b-162">AOF 지속성</span><span class="sxs-lookup"><span data-stu-id="2017b-162">AOF persistence</span></span>
* [<span data-ttu-id="2017b-163">두 번째 저장소 계정은 언제 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-163">When should I use a second storage account?</span></span>](#when-should-i-use-a-second-storage-account)
* [<span data-ttu-id="2017b-164">AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-164">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [<span data-ttu-id="2017b-165">Hello 두 번째 저장소 계정을 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2017b-165">How can I remove hello second storage account?</span></span>](#how-can-i-remove-the-second-storage-account)
* [<span data-ttu-id="2017b-166">다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-166">What is a rewrite and how does it affect my cache?</span></span>](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [<span data-ttu-id="2017b-167">AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-167">What should I expect when scaling a cache with AOF enabled?</span></span>](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [<span data-ttu-id="2017b-168">저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-168">How is my AOF data organized in storage?</span></span>](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a><span data-ttu-id="2017b-169">이전에 만든 캐시에서 지속성을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-169">Can I enable persistence on a previously created cache?</span></span>
<span data-ttu-id="2017b-170">예, Redis 지속성은 캐시를 만들 때와 기존 프리미엄 캐시에서 모두 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-170">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span></span>

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a><span data-ttu-id="2017b-171">사용할 수 있습니까 hello에서 AOF 및 RDB 지 속성 동시?</span><span class="sxs-lookup"><span data-stu-id="2017b-171">Can I enable AOF and RDB persistence at hello same time?</span></span>

<span data-ttu-id="2017b-172">아니요,만 RDB 또는 AOF, 하나만 hello에를 사용할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-172">No, you can enable only RDB or AOF, but not both at hello same time.</span></span>

### <a name="which-persistence-model-should-i-choose"></a><span data-ttu-id="2017b-173">어떤 지속성 모델을 선택해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-173">Which persistence model should I choose?</span></span>

<span data-ttu-id="2017b-174">처리량에 대 한 몇 가지 영향이 있는 모든 쓰기 tooa 로그를 저장 하는 AOF 지 속성, RDB와 비교 hello에 따라 백업을 저장 하는 지 속성 구성 백업 간격 성능에 미치는 영향을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-174">AOF persistence saves every write tooa log, which has some impact on throughput, compared with RDB persistence which saves backups based on hello configured backup interval, with minimal impact on performance.</span></span> <span data-ttu-id="2017b-175">주요 목표는 toominimize 데이터 손실, 프로그램과 캐시에 대 한 처리량이 감소를 처리할 수 있는 경우에 AOF 지 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-175">Choose AOF persistence if your primary goal is toominimize data loss, and you can handle a decrease in throughput for your cache.</span></span> <span data-ttu-id="2017b-176">캐시에 toomaintain 최적 처리량을 원하는 하지만 계속 데이터 복구 하기 위한 메커니즘을 실행할 경우 RDB 지 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-176">Choose RDB persistence if you wish toomaintain optimal throughput on your cache, but still want a mechanism for data recovery.</span></span>

* <span data-ttu-id="2017b-177">Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages) RDB 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-177">Learn more about hello [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="2017b-178">Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages) AOF 지 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-178">Learn more about hello [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="2017b-179">AOF 지속성을 사용하는 경우 성능에 대한 자세한 내용은 [AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2017b-179">For more information on performance when using AOF persistence, see [Does AOF persistence affect throughout, latency, or performance of my cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span></span>

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a><span data-ttu-id="2017b-180">Tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="2017b-180">What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?</span></span>

<span data-ttu-id="2017b-181">RDB 및 AOF 지속성:</span><span class="sxs-lookup"><span data-stu-id="2017b-181">For both RDB and AOF persistence:</span></span>

* <span data-ttu-id="2017b-182">Tooa 더 큰 크기를 조정 했을 경우 아무 영향도 끼치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-182">If you have scaled tooa larger size, there is no impact.</span></span>
* <span data-ttu-id="2017b-183">Tooa 더 작은 크기를 조정 했 고 사용자 지정 [데이터베이스](cache-configure.md#databases) hello 보다 크면 설정 [데이터베이스 제한](cache-configure.md#databases) 복원 되지 않으면 해당 데이터베이스의 데이터에 새 크기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-183">If you have scaled tooa smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than hello [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't restored.</span></span> <span data-ttu-id="2017b-184">자세한 내용은 [사용자 지정 데이터베이스 설정이 크기 조정 동안 영향을 받나요?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span><span class="sxs-lookup"><span data-stu-id="2017b-184">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span></span>
* <span data-ttu-id="2017b-185">Tooa 더 작은 크기를 조정 했 hello 더 작은 크기 toohold 모든 hello 데이터 hello 마지막 백업, 키를 제거 하는 hello 복원 프로세스 중에 충분 한 공간이 없는 경우 일반적으로 사용 하 여 hello [allkeys lru](http://redis.io/topics/lru-cache) 제거 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-185">If you have scaled tooa smaller size, and there isn't enough room in hello smaller size toohold all of hello data from hello last backup, keys will be evicted during hello restore process, typically using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span>

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a><span data-ttu-id="2017b-186">Hello 캐시를 만든 후 hello RDB 백업 빈도 변경 합니까?</span><span class="sxs-lookup"><span data-stu-id="2017b-186">Can I change hello RDB backup frequency after I create hello cache?</span></span>
<span data-ttu-id="2017b-187">예, hello hello에 RDB 지 속성에 대 한 백업 빈도 변경할 수 있습니다 **Redis 데이터 지 속성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-187">Yes, you can change hello backup frequency for RDB persistence on hello **Redis data persistence** blade.</span></span> <span data-ttu-id="2017b-188">자세한 내용은 [Redis 지속성 구성](#configure-redis-persistence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2017b-188">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span></span>

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a><span data-ttu-id="2017b-189">RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-189">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>
<span data-ttu-id="2017b-190">hello RDB 지 속성 백업 빈도 간격 hello 이전 백업 프로세스가 성공적으로 완료 될 때까지 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-190">hello RDB persistence backup frequency interval does not start until hello previous backup process has completed successfully.</span></span> <span data-ttu-id="2017b-191">Hello 백업 빈도 제한은 60 분 하는 경우 전체 백업 프로세스가 15 분 toosuccessfully 걸리는 hello 다음 백업 hello 후 75 분의 시작 시간 hello 이전 백업 될 때까지 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-191">If hello backup frequency is 60 minutes and it takes a backup process 15 minutes toosuccessfully complete, hello next backup won't start until 75 minutes after hello start time of hello previous backup.</span></span>

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a><span data-ttu-id="2017b-192">새 백업을 만들어질 때 toohello 오래 RDB 백업 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-192">What happens toohello old RDB backups when a new backup is made?</span></span>
<span data-ttu-id="2017b-193">가장 최근의 hello 제외한 모든 RDB 지 속성 백업은 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-193">All RDB persistence backups except for hello most recent one are automatically deleted.</span></span> <span data-ttu-id="2017b-194">즉시 삭제되지 않을 수 있으나 오래된 백업을 무한정 유지하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-194">This deletion may not happen immediately but older backups are not persisted indefinitely.</span></span>


### <a name="when-should-i-use-a-second-storage-account"></a><span data-ttu-id="2017b-195">두 번째 저장소 계정은 언제 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-195">When should I use a second storage account?</span></span>

<span data-ttu-id="2017b-196">Hello 캐시에 대 한 예상된 설정 작업 보다 더 높은 있다고 판단 되 면 AOF 지 속성에 대 한 두 번째 저장소 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-196">You should use a second storage account for AOF persistence when you believe you have higher than expected set operations on hello cache.</span></span>  <span data-ttu-id="2017b-197">Hello 보조 저장소 계정 설정을 사용 하는 캐시 저장소 대역폭 제한에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-197">Setting up hello secondary storage account helps ensure your cache doesn't reach storage bandwidth limits.</span></span>

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a><span data-ttu-id="2017b-198">AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-198">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>

<span data-ttu-id="2017b-199">AOF 지 속성에 영향을 줍니다 처리량으로 약 15%-20% 최대 부하 미달 hello 캐시 하는 경우 (CPU 및 서버 부하 둘 다의 90%).</span><span class="sxs-lookup"><span data-stu-id="2017b-199">AOF persistence affects throughput by about 15% – 20% when hello cache is below maximum load (CPU and Server Load both under 90%).</span></span> <span data-ttu-id="2017b-200">Hello 캐시 이러한 한도 내에 있을 때 대기 시간 문제 되지 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-200">There should not be latency issues when hello cache is within these limits.</span></span> <span data-ttu-id="2017b-201">그러나 hello 캐시 됩니다 이러한 한도 더 빨리에 도달할 AOF 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-201">However, hello cache will reach these limits sooner with AOF enabled.</span></span>

### <a name="how-can-i-remove-hello-second-storage-account"></a><span data-ttu-id="2017b-202">Hello 두 번째 저장소 계정을 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2017b-202">How can I remove hello second storage account?</span></span>

<span data-ttu-id="2017b-203">Hello toobe hello 동일 hello 첫 번째 저장소 계정으로는 두 번째 저장소 계정을 설정 하 여 hello AOF 지 속성 보조 저장소 계정을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-203">You can remove hello AOF persistence secondary storage account by setting hello second storage account toobe hello same as hello first storage account.</span></span> <span data-ttu-id="2017b-204">자세한 내용은 [AOF 지속성 구성](#configure-aof-persistence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2017b-204">For instructions, see [Configure AOF persistence](#configure-aof-persistence).</span></span>

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a><span data-ttu-id="2017b-205">다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-205">What is a rewrite and how does it affect my cache?</span></span>

<span data-ttu-id="2017b-206">Hello AOF 파일 충분 해지면에서 다시 작성 hello 캐시에서 자동으로 대기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-206">When hello AOF file becomes large enough, a rewrite is automatically queued on hello cache.</span></span> <span data-ttu-id="2017b-207">hello 재작성 크기가 조정 되어 hello AOF 파일 hello 최소한 필요한 작업 toocreate hello 현재 데이터 집합의 집합으로입니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-207">hello rewrite resizes hello AOF file with hello minimal set of operations needed toocreate hello current data set.</span></span> <span data-ttu-id="2017b-208">를 캡슐화 하는 동안 큰 데이터 집합으로 처리할 때 tooreach 성능 한도 더 빨리 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-208">During rewrites, expect tooreach performance limits sooner especially when dealing with large datasets.</span></span> <span data-ttu-id="2017b-209">다시 작성이 이벤트가 발생 작은 종종 hello AOF 파일, 더 큰 수 없지만 때 자주 발생 하는 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-209">Rewrites occur less often as hello AOF file becomes larger, but will take a significant amount of time when it happens.</span></span>

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a><span data-ttu-id="2017b-210">AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-210">What should I expect when scaling a cache with AOF enabled?</span></span>

<span data-ttu-id="2017b-211">크기 조정의 hello 시 hello AOF 파일 훨씬 큰 경우에 다음 hello 크기 조정 작업 tootake 것은 수 파일을 다시 로드 hello 크기 조정을 마친 후 이후 예상 보다 오래 것 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-211">If hello AOF file at hello time of scaling is significantly large, then expect hello scale operation tootake longer than expected since it will be reloading hello file after scaling has finished.</span></span>

<span data-ttu-id="2017b-212">확장에 대 한 자세한 내용은 참조 하십시오. [tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하면 어떻게 되나요?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span><span class="sxs-lookup"><span data-stu-id="2017b-212">For more information on scaling, see [What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span></span>

### <a name="how-is-my-aof-data-organized-in-storage"></a><span data-ttu-id="2017b-213">저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?</span><span class="sxs-lookup"><span data-stu-id="2017b-213">How is my AOF data organized in storage?</span></span>

<span data-ttu-id="2017b-214">AOF 파일에 저장 된 데이터는 hello 데이터 toostorage 저장 노드 tooincrease 성능 당 여러 페이지 blob으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-214">Data stored in AOF files is divided into multiple page blobs per node tooincrease performance of saving hello data toostorage.</span></span> <span data-ttu-id="2017b-215">hello 다음 표에 표시 페이지 blob 수는 각 가격 책정 계층에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-215">hello following table displays how many page blobs are used for each pricing tier:</span></span>

| <span data-ttu-id="2017b-216">프리미엄 계층</span><span class="sxs-lookup"><span data-stu-id="2017b-216">Premium tier</span></span> | <span data-ttu-id="2017b-217">Blob</span><span class="sxs-lookup"><span data-stu-id="2017b-217">Blobs</span></span> |
|--------------|-------|
| <span data-ttu-id="2017b-218">P1</span><span class="sxs-lookup"><span data-stu-id="2017b-218">P1</span></span>           | <span data-ttu-id="2017b-219">분할당 4</span><span class="sxs-lookup"><span data-stu-id="2017b-219">4 per shard</span></span>    |
| <span data-ttu-id="2017b-220">P2</span><span class="sxs-lookup"><span data-stu-id="2017b-220">P2</span></span>           | <span data-ttu-id="2017b-221">분할당 8</span><span class="sxs-lookup"><span data-stu-id="2017b-221">8 per shard</span></span>    |
| <span data-ttu-id="2017b-222">P3</span><span class="sxs-lookup"><span data-stu-id="2017b-222">P3</span></span>           | <span data-ttu-id="2017b-223">분할당 16</span><span class="sxs-lookup"><span data-stu-id="2017b-223">16 per shard</span></span>   |
| <span data-ttu-id="2017b-224">P4</span><span class="sxs-lookup"><span data-stu-id="2017b-224">P4</span></span>           | <span data-ttu-id="2017b-225">분할당 20</span><span class="sxs-lookup"><span data-stu-id="2017b-225">20 per shard</span></span>   |

<span data-ttu-id="2017b-226">클러스터링을 사용 하면 hello 캐시에 있는 각 분할에 hello 이전 표에 표시 된 페이지 blob 자체 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-226">When clustering is enabled, each shard in hello cache has its own set of page blobs, as indicated in hello previous table.</span></span> <span data-ttu-id="2017b-227">예를 들어 분할이 3개 있는 P2 캐시는 24개 페이지 Blob에 해당 AOF 파일을 분산합니다(분할당 8 Blob, 3개 분할).</span><span class="sxs-lookup"><span data-stu-id="2017b-227">For example, a P2 cache with three shards distributes its AOF file across 24 page blobs (8 blobs per shard, with 3 shards).</span></span>

<span data-ttu-id="2017b-228">다시 쓰기 후 2개의 AOF 파일 집합이 저장소에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-228">After a rewrite, two sets of AOF files exist in storage.</span></span> <span data-ttu-id="2017b-229">Hello 백그라운드에서 발생 하 고 hello 다시 쓰는 동안 toohello 캐시 전송 되는 집합 작업이 toohello 두 번째 세트를 추가 하는 동안 toohello 파일의 첫 번째 집합을 추가 하는 다시 작성 하세요.</span><span class="sxs-lookup"><span data-stu-id="2017b-229">Rewrites occur in hello background and append toohello first set of files, while set operations that are sent toohello cache during hello rewrite append toohello second set.</span></span> <span data-ttu-id="2017b-230">오류가 발생한 경우 백업은 다시 쓰기 동안 일시적으로 저장되지만 다시 쓰기가 끝난 후에 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-230">A backup is temporarily stored during rewrites in case of failure, but is promptly deleted after a rewrite finishes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2017b-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2017b-231">Next steps</span></span>
<span data-ttu-id="2017b-232">Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2017b-232">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="2017b-233">Toohello Azure Redis Cache 프리미엄 계층 소개</span><span class="sxs-lookup"><span data-stu-id="2017b-233">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png

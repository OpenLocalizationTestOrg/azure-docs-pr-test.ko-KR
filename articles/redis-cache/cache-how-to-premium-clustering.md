---
title: "프리미엄 Azure Redis Cache에 대 한 클러스터링 aaaHow tooconfigure Redis | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 Redis 클러스터링은 고급 계층에 대 한 Azure Redis Cache 인스턴스 관리"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a><span data-ttu-id="c272d-103">Tooconfigure Redis Premium Azure Redis Cache에 대 한 클러스터링 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c272d-103">How tooconfigure Redis clustering for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="c272d-104">Azure Redis 캐시 캐시 크기 및 기능, 프리미엄 계층 기능 클러스터링, 지 속성 및 가상 네트워크 지원 등을 포함 하 여 hello 선택에서 유연성을 제공 하는 다른 캐시 기능에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="c272d-105">이 문서에서는 Azure Redis 캐시 하는 클러스터링에 프리미엄 tooconfigure 방법 설명 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="c272d-105">This article describes how tooconfigure clustering in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="c272d-106">다른 프리미엄 캐시 기능에 대 한 자세한 내용은 참조 [toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-106">For information on other premium cache features, see [Introduction toohello Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-redis-cluster"></a><span data-ttu-id="c272d-107">Redis 클러스터란?</span><span class="sxs-lookup"><span data-stu-id="c272d-107">What is Redis Cluster?</span></span>
<span data-ttu-id="c272d-108">Azure Redis Cache는 [Redis에서 구현된 형태의](http://redis.io/topics/cluster-tutorial)Redis 클러스터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-108">Azure Redis Cache offers Redis cluster as [implemented in Redis](http://redis.io/topics/cluster-tutorial).</span></span> <span data-ttu-id="c272d-109">Redis 클러스터와 hello 다음 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-109">With Redis Cluster, you get hello following benefits:</span></span> 

* <span data-ttu-id="c272d-110">hello 기능 tooautomatically 여러 노드 중에서 데이터 집합을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-110">hello ability tooautomatically split your dataset among multiple nodes.</span></span> 
* <span data-ttu-id="c272d-111">오류 발생 또는 없습니다 toocommunicate hello 나머지 hello 클러스터와는 hello 기능 toocontinue 작업 때 하위 집합 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="c272d-111">hello ability toocontinue operations when a subset of hello nodes is experiencing failures or are unable toocommunicate with hello rest of hello cluster.</span></span> 
* <span data-ttu-id="c272d-112">더 많은 처리량: hello 분할 영역 수를 늘리면 처리량 선형으로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-112">More throughput: Throughput increases linearly as you increase hello number of shards.</span></span> 
* <span data-ttu-id="c272d-113">더 많은 메모리 크기: hello 분할 영역 수를 늘리면 비례하여 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-113">More memory size: Increases linearly as you increase hello number of shards.</span></span>  

<span data-ttu-id="c272d-114">프리미엄 캐시에서의 크기, 처리량 및 대역폭에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-114">For more information about size, throughput, and bandwidth with premium caches, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>

<span data-ttu-id="c272d-115">Azure Redis 클러스터는 각 분할 된 데이터베이스에 있는 복제의 경우 주/복제본 쌍 hello 복제 Azure Redis 캐시 서비스에서 관리 되는 위치는 주/복제본 모델로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-115">In Azure, Redis cluster is offered as a primary/replica model where each shard has a primary/replica pair with replication where hello replication is managed by Azure Redis Cache service.</span></span> 

## <a name="clustering"></a><span data-ttu-id="c272d-116">클러스터링</span><span class="sxs-lookup"><span data-stu-id="c272d-116">Clustering</span></span>
<span data-ttu-id="c272d-117">Hello에서 클러스터링을 사용할 수 **새 Redis 캐시** 블레이드 캐시 만들기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-117">Clustering is enabled on hello **New Redis Cache** blade during cache creation.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="c272d-118">Hello에 구성 된 클러스터링 **Redis 클러스터** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-118">Clustering is configured on hello **Redis Cluster** blade.</span></span>

![클러스터링][redis-cache-clustering]

<span data-ttu-id="c272d-120">Too10 hello 클러스터의 분할 된 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-120">You can have up too10 shards in hello cluster.</span></span> <span data-ttu-id="c272d-121">클릭 **Enabled** hello 슬라이더를 이동 하거나 1과 10 사이의 숫자를 입력 하 고 **분할 영역 수** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-121">Click **Enabled** and slide hello slider or type a number between 1 and 10 for **Shard count** and click **OK**.</span></span>

<span data-ttu-id="c272d-122">각 분할은 Azure에서 관리 되는 주/복제본 캐시 쌍 및 hello 캐시의 총 크기가 hello hello 분할 영역 수 hello 가격 책정 계층에서에서 선택한 hello 캐시 크기를 곱하여 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-122">Each shard is a primary/replica cache pair managed by Azure, and hello total size of hello cache is calculated by multiplying hello number of shards by hello cache size selected in hello pricing tier.</span></span> 

![클러스터링][redis-cache-clustering-selected]

<span data-ttu-id="c272d-124">Hello 캐시는 생성 되 면 tooit 연결 하 고 사용 하 여 방금가 클러스터 되지 않은 캐시와 유사 하 고 Redis hello 캐시 분할 된 데이터베이스 전체의 hello 데이터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-124">Once hello cache is created you connect tooit and use it just like a non-clustered cache, and Redis distributes hello data throughout hello Cache shards.</span></span> <span data-ttu-id="c272d-125">진단이 [활성화](cache-how-to-monitor.md#enable-cache-diagnostics), 메트릭 각 분할에 대해 개별적으로 문서화 하 고 수 [볼](cache-how-to-monitor.md) hello Redis 캐시 블레이드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-125">If diagnostics is [enabled](cache-how-to-monitor.md#enable-cache-diagnostics), metrics are captured separately for each shard and can be [viewed](cache-how-to-monitor.md) in hello Redis Cache blade.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="c272d-126">클러스터링을 구성할 때 클라이언트 응용 프로그램에 필요한 몇 가지 사소한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-126">There are some minor differences required in your client application when clustering is configured.</span></span> <span data-ttu-id="c272d-127">자세한 내용은 참조 [필요 합니까 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="c272d-127">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>
> 
> 

<span data-ttu-id="c272d-128">Hello StackExchange.Redis 클라이언트를 사용한 클러스터링 사용에 대 한 샘플 코드에서 참조 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello 부분의 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.</span><span class="sxs-lookup"><span data-stu-id="c272d-128">For sample code on working with clustering with hello StackExchange.Redis client, see hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a><span data-ttu-id="c272d-129">실행 하는에서 hello 클러스터 크기를 변경 합니다. 프리미엄 캐시</span><span class="sxs-lookup"><span data-stu-id="c272d-129">Change hello cluster size on a running premium cache</span></span>
<span data-ttu-id="c272d-130">실행 중인 프리미엄에 대 한 toochange hello 클러스터 크기 클러스터링 사용된을 클릭 하 여 캐시 **Redis 클러스터 크기** hello에서 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-130">toochange hello cluster size on a running premium cache with clustering enabled, click **Redis Cluster Size** from hello **Resource menu**.</span></span>

> [!NOTE]
> <span data-ttu-id="c272d-131">Hello Azure Redis Cache 프리미엄 계층 되었습니다 해제 tooGeneral 가용성 동안 hello Redis 클러스터 크기 기능은 현재 미리 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-131">While hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 클러스터 크기][redis-cache-redis-cluster-size]

<span data-ttu-id="c272d-133">toochange hello 클러스터 크기 hello 슬라이더를 사용 하거나 hello에 1과 10 사이의 숫자를 입력 **분할 영역 수** 텍스트 상자 **확인** toosave 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-133">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!NOTE]
> <span data-ttu-id="c272d-134">Hello를 실행 하는 클러스터 크기 조정 [마이그레이션](https://redis.io/commands/migrate) 비용이 많이 드는 명령 인 명령의 최소한의 영향에 대 한 것이 좋습니다 사용량이 적은 시간 중에이 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-134">Scaling a cluster runs hello [MIGRATE](https://redis.io/commands/migrate) command, which is an expensive command, so for minimal impact, consider running this operation during non-peak hours.</span></span> <span data-ttu-id="c272d-135">Hello 마이그레이션 프로세스 중 서버 부하에 스파이크가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-135">During hello migration process, you will see a spike in server load.</span></span> <span data-ttu-id="c272d-136">클러스터를 확장 하는 장기 실행 중인 프로세스 및 hello에 걸린 시간에 따라 달라 집니다 hello 키 수와 해당 키와 관련 된 hello 값의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-136">Scaling a cluster is a long running process and hello amount of time taken depends on hello number of keys and size of hello values associated with those keys.</span></span>
> 
> 

## <a name="clustering-faq"></a><span data-ttu-id="c272d-137">클러스터링 FAQ</span><span class="sxs-lookup"><span data-stu-id="c272d-137">Clustering FAQ</span></span>
<span data-ttu-id="c272d-138">hello 다음 목록에 포함 되어 Azure Redis Cache 클러스터링에 대 한 질문과 대답 toocommonly 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-138">hello following list contains answers toocommonly asked questions about Azure Redis Cache clustering.</span></span>

* [<span data-ttu-id="c272d-139">해야 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?</span><span class="sxs-lookup"><span data-stu-id="c272d-139">Do I need toomake any changes toomy client application toouse clustering?</span></span>](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [<span data-ttu-id="c272d-140">클러스터에서 키를 분산하는 방법</span><span class="sxs-lookup"><span data-stu-id="c272d-140">How are keys distributed in a cluster?</span></span>](#how-are-keys-distributed-in-a-cluster)
* [<span data-ttu-id="c272d-141">만들 수 있습니다. hello 최대 캐시 크기는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-141">What is hello largest cache size I can create?</span></span>](#what-is-the-largest-cache-size-i-can-create)
* [<span data-ttu-id="c272d-142">모든 Redis 클라이언트가 클러스터링을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-142">Do all Redis clients support clustering?</span></span>](#do-all-redis-clients-support-clustering)
* [<span data-ttu-id="c272d-143">클러스터링을 사용 하는 toomy 캐시를 연결 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c272d-143">How do I connect toomy cache when clustering is enabled?</span></span>](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [<span data-ttu-id="c272d-144">직접 내 캐시의 분할 된 toohello 개별 데이터베이스를 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-144">Can I directly connect toohello individual shards of my cache?</span></span>](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [<span data-ttu-id="c272d-145">이전에 만든된 캐시에 대해 클러스터링을 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-145">Can I configure clustering for a previously created cache?</span></span>](#can-i-configure-clustering-for-a-previously-created-cache)
* [<span data-ttu-id="c272d-146">기본 또는 표준 캐시에 클러스터링을 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-146">Can I configure clustering for a basic or standard cache?</span></span>](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [<span data-ttu-id="c272d-147">클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-147">Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?</span></span>](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [<span data-ttu-id="c272d-148">StackExchange.Redis를 사용하고 클러스터링을 수행할 때 MOVE 예외가 발생합니다. 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-148">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a><span data-ttu-id="c272d-149">해야 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?</span><span class="sxs-lookup"><span data-stu-id="c272d-149">Do I need toomake any changes toomy client application toouse clustering?</span></span>
* <span data-ttu-id="c272d-150">클러스터링 사용하는 경우 데이터베이스 0만을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-150">When clustering is enabled, only database 0 is available.</span></span> <span data-ttu-id="c272d-151">클라이언트 응용 프로그램에서 여러 데이터베이스를 사용 하는 경우 0이 아닌 tooa 데이터베이스 tooread 또는 쓰기를 시도 하기 hello 다음 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-151">If your client application uses multiple databases and it tries tooread or write tooa database other than 0, hello following exception is thrown.</span></span> <span data-ttu-id="c272d-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`</span><span class="sxs-lookup"><span data-stu-id="c272d-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`</span></span>
  
  <span data-ttu-id="c272d-153">자세한 내용은 [Redis 클러스터 사양 - 구현된 하위 집합](http://redis.io/topics/cluster-spec#implemented-subset)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-153">For more information, see [Redis Cluster Specification - Implemented subset](http://redis.io/topics/cluster-spec#implemented-subset).</span></span>
* <span data-ttu-id="c272d-154">[StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/)를 사용하는 경우 1.0.481 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-154">If you are using [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), you must use 1.0.481 or later.</span></span> <span data-ttu-id="c272d-155">Toohello 캐시 연결 동일 hello를 사용 하 여 [끝점, 포트 및 키](cache-configure.md#properties) 클러스터링을 사용 하지 않은 tooa 캐시를 연결할 때 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-155">You connect toohello cache using hello same [endpoints, ports, and keys](cache-configure.md#properties) that you use when connecting tooa cache that does not have clustering enabled.</span></span> <span data-ttu-id="c272d-156">hello 유일한 차이점은 모든 읽기 및 쓰기 수행 해야 함을 toodatabase 0입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-156">hello only difference is that all reads and writes must be done toodatabase 0.</span></span>
  
  * <span data-ttu-id="c272d-157">다른 클라이언트는 다른 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-157">Other clients may have different requirements.</span></span> <span data-ttu-id="c272d-158">[모든 Redis 클라이언트가 클러스터링을 지원하나요?](#do-all-redis-clients-support-clustering)</span><span class="sxs-lookup"><span data-stu-id="c272d-158">See [Do all Redis clients support clustering?](#do-all-redis-clients-support-clustering)</span></span>
* <span data-ttu-id="c272d-159">응용 프로그램에서 단일 명령으로 일괄 처리할 여러 개의 키 작업을 사용 하는 경우 모든 키에 있어야 hello 동일한 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-159">If your application uses multiple key operations batched into a single command, all keys must be located in hello same shard.</span></span> <span data-ttu-id="c272d-160">toolocate 키에서 동일한 shard hello 하 참조 [클러스터에서 키는 배포 방법을?](#how-are-keys-distributed-in-a-cluster)</span><span class="sxs-lookup"><span data-stu-id="c272d-160">toolocate keys in hello same shard, see [How are keys distributed in a cluster?](#how-are-keys-distributed-in-a-cluster)</span></span>
* <span data-ttu-id="c272d-161">Redis ASP.NET 세션 상태 제공자를 사용하는 경우 2.0.1 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-161">If you are using Redis ASP.NET Session State provider you must use 2.0.1 or higher.</span></span> <span data-ttu-id="c272d-162">참조 [클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span><span class="sxs-lookup"><span data-stu-id="c272d-162">See [Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span></span>

### <a name="how-are-keys-distributed-in-a-cluster"></a><span data-ttu-id="c272d-163">클러스터에서 키를 분산하는 방법</span><span class="sxs-lookup"><span data-stu-id="c272d-163">How are keys distributed in a cluster?</span></span>
<span data-ttu-id="c272d-164">Hello Redis 당 [키 배포 모델](http://redis.io/topics/cluster-spec#keys-distribution-model) 설명서: hello 키 공간 16384 슬롯으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-164">Per hello Redis [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model) documentation: hello key space is split into 16384 slots.</span></span> <span data-ttu-id="c272d-165">각 키는 해시 이며 tooone hello 클러스터의 노드를 hello 통해 배포 되는 이러한 슬롯을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-165">Each key is hashed and assigned tooone of these slots, which are distributed across hello nodes of hello cluster.</span></span> <span data-ttu-id="c272d-166">Hello 키의 어느 부분이 여러 키에 있는 해시 된 tooensure 구성할 수는 해시 태그를 사용 하는 동일한 분할 영역 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-166">You can configure which part of hello key is hashed tooensure that multiple keys are located in hello same shard using hash tags.</span></span>

* <span data-ttu-id="c272d-167">Hello 키의 일부에 포함 되어 있으면 해시 태그-와 키는 `{` 및 `}`, hello 키의 해당 부분에만 키의 해시 슬롯 hello를 결정 하는 hello로 해시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-167">Keys with a hash tag - if any part of hello key is enclosed in `{` and `}`, only that part of hello key is hashed for hello purposes of determining hello hash slot of a key.</span></span> <span data-ttu-id="c272d-168">Hello에 다음 3 개의 키 hello은 위치 하는 예를 들어 동일한 shard: `{key}1`, `{key}2`, 및 `{key}3` 만 hello 이후 `key` hello 이름의 일부 해시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-168">For example, hello following 3 keys would be located in hello same shard: `{key}1`, `{key}2`, and `{key}3` since only hello `key` part of hello name is hashed.</span></span> <span data-ttu-id="c272d-169">키 해시 태그 사양의 전체 목록은 [키 해시 태그](http://redis.io/topics/cluster-spec#keys-hash-tags)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-169">For a complete list of keys hash tag specifications, see [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>
* <span data-ttu-id="c272d-170">해시는 해시 태그-hello 전체 키 이름 없이 키 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-170">Keys without a hash tag - hello entire key name is used for hashing.</span></span> <span data-ttu-id="c272d-171">따라서 hello hello 캐시의 분할 된 데이터베이스에서 통계적으로 균등 한 분포가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-171">This results in a statistically even distribution across hello shards of hello cache.</span></span>

<span data-ttu-id="c272d-172">최상의 성능 및 처리량에 대 한 hello 키를 균등 하 게 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-172">For best performance and throughput, we recommend distributing hello keys evenly.</span></span> <span data-ttu-id="c272d-173">키 해시 태그와 함께 사용 하는 경우 hello 응용 프로그램의 책임 tooensure hello 키는 고르게 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-173">If you are using keys with a hash tag it is hello application's responsibility tooensure hello keys are distributed evenly.</span></span>

<span data-ttu-id="c272d-174">자세한 내용은 [키 배포 모델](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis 클러스터 데이터 분할](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) 및 [키 해시 태그](http://redis.io/topics/cluster-spec#keys-hash-tags)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-174">For more information, see [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis Cluster data sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), and [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>

<span data-ttu-id="c272d-175">샘플 코드와 클러스터링 키 hello에서 찾기 작업에 대 한 hello StackExchange.Redis 클라이언트를 사용 하 여 동일한 분할 참조 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello 부분의 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.</span><span class="sxs-lookup"><span data-stu-id="c272d-175">For sample code on working with clustering and locating keys in hello same shard with hello StackExchange.Redis client, see hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

### <a name="what-is-hello-largest-cache-size-i-can-create"></a><span data-ttu-id="c272d-176">만들 수 있습니다. hello 최대 캐시 크기는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-176">What is hello largest cache size I can create?</span></span>
<span data-ttu-id="c272d-177">hello 가장 큰 premium 캐시 크기는 53 GB입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-177">hello largest premium cache size is 53 GB.</span></span> <span data-ttu-id="c272d-178">Too10 분할 530 g B의 최대 크기를 지정 된 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-178">You can create up too10 shards giving you a maximum size of 530 GB.</span></span> <span data-ttu-id="c272d-179">더 큰 크기가 필요한 경우 [추가 요청](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase)이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-179">If you need a larger size you can [request more](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase).</span></span> <span data-ttu-id="c272d-180">자세한 내용은 [Azure Redis Cache 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-180">For more information, see [Azure Redis Cache Pricing](https://azure.microsoft.com/pricing/details/cache/).</span></span>

### <a name="do-all-redis-clients-support-clustering"></a><span data-ttu-id="c272d-181">모든 Redis 클라이언트가 클러스터링을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-181">Do all Redis clients support clustering?</span></span>
<span data-ttu-id="c272d-182">Hello에서 모든 클라이언트에서 지원 되는 현재 시간 Redis 클러스터링 사용.</span><span class="sxs-lookup"><span data-stu-id="c272d-182">At hello present time not all clients support Redis clustering.</span></span> <span data-ttu-id="c272d-183">이를 지원하는 클라이언트는 StackExchange.Redis입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-183">StackExchange.Redis is one that does support for it.</span></span> <span data-ttu-id="c272d-184">다른 클라이언트에 자세한 내용은 참조 hello [hello 클러스터와 재생](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) hello 섹션 [Redis 클러스터 자습서](http://redis.io/topics/cluster-tutorial)합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-184">For more information on other clients, see hello [Playing with hello cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) section of hello [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

> [!NOTE]
> <span data-ttu-id="c272d-185">StackExchange.Redis 클라이언트를 사용 하는 경우 최신 버전의 hello를 사용 하는 확인 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 올바르게 toowork 클러스터링에 대 한 이상.</span><span class="sxs-lookup"><span data-stu-id="c272d-185">If you are using StackExchange.Redis as your client, ensure you are using hello latest version of [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 or later for clustering toowork correctly.</span></span> <span data-ttu-id="c272d-186">move 예외에 문제가 있을 경우 자세한 내용은 [move 예외](#move-exceptions) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-186">If you have any issues with move exceptions, see [move exceptions](#move-exceptions) for more information.</span></span>
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a><span data-ttu-id="c272d-187">클러스터링을 사용 하는 toomy 캐시를 연결 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c272d-187">How do I connect toomy cache when clustering is enabled?</span></span>
<span data-ttu-id="c272d-188">Tooyour 캐시 연결 수 동일 hello를 사용 하 여 [끝점](cache-configure.md#properties), [포트](cache-configure.md#properties), 및 [키](cache-configure.md#access-keys) 클러스터링을 사용 하지 않은 tooa 캐시를 연결할 때 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-188">You can connect tooyour cache using hello same [endpoints](cache-configure.md#properties), [ports](cache-configure.md#properties), and [keys](cache-configure.md#access-keys) that you use when connecting tooa cache that does not have clustering enabled.</span></span> <span data-ttu-id="c272d-189">Redis hello toomanage 없는 hello 백 엔드에 클러스터링 관리 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="c272d-189">Redis manages hello clustering on hello backend so you don't have toomanage it from your client.</span></span>

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a><span data-ttu-id="c272d-190">직접 내 캐시의 분할 된 toohello 개별 데이터베이스를 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-190">Can I directly connect toohello individual shards of my cache?</span></span>
<span data-ttu-id="c272d-191">공식적으로는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-191">This is not officially supported.</span></span> <span data-ttu-id="c272d-192">즉 각각의 분할된 데이터베이스는 캐시 인스턴스로 통칭되는 주/복제본 캐시로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-192">With that said, each shard consists of a primary/replica cache pair, collectively known as a cache instance.</span></span> <span data-ttu-id="c272d-193">Hello redis cli 유틸리티를 사용 하 여 hello에 toothese 캐시 인스턴스를 연결할 수 있습니다 [불안정](http://redis.io/download) GitHub에서 hello Redis 리포지토리의 분기입니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-193">You can connect toothese cache instances using hello redis-cli utility in hello [unstable](http://redis.io/download) branch of hello Redis repository at GitHub.</span></span> <span data-ttu-id="c272d-194">이 버전 hello로 시작 될 때 기본 지원을 구현 `-c` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-194">This version implements basic support when started with hello `-c` switch.</span></span> <span data-ttu-id="c272d-195">자세한 내용은 참조 [hello 클러스터와 재생](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) 에 [http://redis.io](http://redis.io) hello에 [Redis 클러스터 자습서](http://redis.io/topics/cluster-tutorial)합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-195">For more information see [Playing with hello cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) on [http://redis.io](http://redis.io) in hello [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

<span data-ttu-id="c272d-196">비 ssl에 대 한 명령을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-196">For non-ssl, use hello following commands.</span></span>

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

<span data-ttu-id="c272d-197">SSL에서는 `1300N`을 `1500N`으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-197">For ssl, replace `1300N` with `1500N`.</span></span>

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a><span data-ttu-id="c272d-198">이전에 만든된 캐시에 대해 클러스터링을 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-198">Can I configure clustering for a previously created cache?</span></span>
<span data-ttu-id="c272d-199">현재 캐시를 만들 때만 클러스터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-199">Currently you can only enable clustering when you create a cache.</span></span> <span data-ttu-id="c272d-200">클러스터링 tooa 프리미엄 캐시를 추가 하거나 hello 캐시는 생성 후 프리미엄 캐시에서 클러스터링을 제거할 수 있지만 hello 캐시를 만든 후 hello 클러스터 크기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-200">You can change hello cluster size after hello cache is created, but you can't add clustering tooa premium cache or remove clustering from a premium cache after hello cache is created.</span></span> <span data-ttu-id="c272d-201">클러스터링을 사용 및 하나의 분할만 프리미엄 캐시는 hello 없는 클러스터링과 함께 동일한 크기의 프리미엄 캐시와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-201">A premium cache with clustering enabled and only one shard is different than a premium cache of hello same size with no clustering.</span></span>

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a><span data-ttu-id="c272d-202">기본 또는 표준 캐시에 클러스터링을 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-202">Can I configure clustering for a basic or standard cache?</span></span>
<span data-ttu-id="c272d-203">클러스터링은 프리미엄 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-203">Clustering is only available for premium caches.</span></span>

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a><span data-ttu-id="c272d-204">클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c272d-204">Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?</span></span>
* <span data-ttu-id="c272d-205">**Redis 출력 캐시 공급자** - 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-205">**Redis Output Cache provider** - no changes required.</span></span>
* <span data-ttu-id="c272d-206">**Redis 세션 상태 공급자** -toouse 클러스터링을 사용 해야 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 높이 거 나 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-206">**Redis Session State provider** - toouse clustering, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="c272d-207">주요 변경 내용입니다. 자세한 내용은 [v2.0.0 주요 변경 세부 사항](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c272d-207">This is a breaking change; for more information see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span>

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a><span data-ttu-id="c272d-208">StackExchange.Redis를 사용하고 클러스터링을 수행할 때 MOVE 예외가 발생합니다. 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c272d-208">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>
<span data-ttu-id="c272d-209">StackExchange.Redis를 사용하고 있으며 클러스터링을 사용할 때 `MOVE` 예외가 발생하는 경우 [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) 이상을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-209">If you are using StackExchange.Redis and receive `MOVE` exceptions when using clustering, ensure that you are using [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) or later.</span></span> <span data-ttu-id="c272d-210">.NET 응용 프로그램 toouse StackExchange.Redis를 구성 하는 방법에 지침은 [hello 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)합니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-210">For instructions on configuring your .NET applications toouse StackExchange.Redis, see [Configure hello cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c272d-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c272d-211">Next steps</span></span>
<span data-ttu-id="c272d-212">Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c272d-212">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="c272d-213">Toohello Azure Redis Cache 프리미엄 계층 소개</span><span class="sxs-lookup"><span data-stu-id="c272d-213">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png








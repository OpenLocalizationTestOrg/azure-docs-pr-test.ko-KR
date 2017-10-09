---
title: "Redis Cache 샘플 aaaAzure | Microsoft Docs"
description: "Azure Redis 캐시 하는 toouse 방법에 대해 알아봅니다"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a><span data-ttu-id="9e710-103">Azure Redis Cache 샘플</span><span class="sxs-lookup"><span data-stu-id="9e710-103">Azure Redis Cache samples</span></span>
<span data-ttu-id="9e710-104">이 항목에서는 Azure Redis Cache 샘플, 예: tooa 캐시 연결, 읽기 및는 캐시에서 데이터 tooand 쓰기 hello ASP.NET Redis 캐시 공급자를 사용 하는 시나리오를 다룹니다 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting tooa cache, reading and writing data tooand from a cache, and using hello ASP.NET Redis Cache providers.</span></span> <span data-ttu-id="9e710-105">Hello 샘플의 일부는 다운로드 가능한 프로젝트 있으며 단계별 지침을 제공 일부 코드 조각을 포함 하지만 tooa 다운로드할 수 있는 프로젝트를 연결 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-105">Some of hello samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link tooa downloadable project.</span></span>

## <a name="hello-world-samples"></a><span data-ttu-id="9e710-106">Hello world 샘플</span><span class="sxs-lookup"><span data-stu-id="9e710-106">Hello world samples</span></span>
<span data-ttu-id="9e710-107">hello이이 섹션의에서 예제에는 Redis 클라이언트를 연결 tooan Azure Redis 캐시 인스턴스를 읽고 쓰는 다양 한 언어를 사용 하 여 데이터 toohello 캐시의 기본 사항 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-107">hello samples in this section show hello basics of connecting tooan Azure Redis Cache instance and reading and writing data toohello cache using a variety of languages and Redis clients.</span></span>

<span data-ttu-id="9e710-108">hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 방법을 보여 줍니다 샘플 tooperform 다양 한 캐시 작업 hello를 사용 하 여 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-108">hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how tooperform various cache operations using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span></span>

<span data-ttu-id="9e710-109">이 샘플에서는 다음 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-109">This sample shows how to:</span></span>

* <span data-ttu-id="9e710-110">다양한 연결 옵션 사용</span><span class="sxs-lookup"><span data-stu-id="9e710-110">Use various connection options</span></span>
* <span data-ttu-id="9e710-111">동기 및 비동기 작업을 사용 하 여 hello 캐시에서 개체 tooand 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="9e710-111">Read and write objects tooand from hello cache using synchronous and asynchronous operations</span></span>
* <span data-ttu-id="9e710-112">지정 된 키의 Redis MGET/MSET 명령을 tooreturn 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9e710-112">Use Redis MGET/MSET commands tooreturn values of specified keys</span></span>
* <span data-ttu-id="9e710-113">Redis 트랜잭션 작업 수행</span><span class="sxs-lookup"><span data-stu-id="9e710-113">Perform Redis transactional operations</span></span>
* <span data-ttu-id="9e710-114">Redis 목록 및 정렬된 집합 작업</span><span class="sxs-lookup"><span data-stu-id="9e710-114">Work with Redis lists and sorted sets</span></span>
* <span data-ttu-id="9e710-115">JsonConvert serializer를 사용하여.NET 개체 저장</span><span class="sxs-lookup"><span data-stu-id="9e710-115">Store .NET objects using JsonConvert serializers</span></span>
* <span data-ttu-id="9e710-116">사용 하 여 Redis 설정 tooimplement 태그 지정</span><span class="sxs-lookup"><span data-stu-id="9e710-116">Use Redis sets tooimplement tagging</span></span>
* <span data-ttu-id="9e710-117">Redis 클러스터 작업</span><span class="sxs-lookup"><span data-stu-id="9e710-117">Work with Redis Cluster</span></span>

<span data-ttu-id="9e710-118">자세한 내용은 참조 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) github와 더 많은 사용 시나리오에 대 한 설명서 참조 hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) 단위 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-118">For more information, see hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span></span>

<span data-ttu-id="9e710-119">[Toouse Azure Redis 캐시 방법 python](cache-python-get-started.md) tooget Python 및 hello를 사용 하 여 Azure Redis 캐시를 시작 하는 방법을 보여 줍니다. [redis py](https://github.com/andymccurdy/redis-py) 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-119">[How toouse Azure Redis Cache with Python](cache-python-get-started.md) shows how tooget started with Azure Redis Cache using Python and hello [redis-py](https://github.com/andymccurdy/redis-py) client.</span></span>

<span data-ttu-id="9e710-120">[Hello 캐시에서.NET 개체 사용](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) tooand 작성할 수 있습니다. 한 가지 방법은 tooserialize.NET 개체에서는 Azure Redis Cache 인스턴스에서 읽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-120">[Work with .NET objects in hello cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way tooserialize .NET objects so you can write them tooand read them from an Azure Redis Cache instance.</span></span> 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a><span data-ttu-id="9e710-121">Redis Cache를 ASP.NET SignalR에 대한 규모 확장 백플레인으로 사용</span><span class="sxs-lookup"><span data-stu-id="9e710-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span></span>
<span data-ttu-id="9e710-122">hello [확장형 백플레인 ASP.NET SignalR 용 Redis Cache 사용](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) 샘플 SignalR 백플레인으로 Azure Redis Cache를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-122">hello [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span></span> <span data-ttu-id="9e710-123">백플레인에 대한 자세한 내용은 [Redis를 사용한 SignalR 규모 확장](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e710-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span></span>

## <a name="redis-cache-customer-query-sample"></a><span data-ttu-id="9e710-124">Redis Cache 고객 쿼리 샘플</span><span class="sxs-lookup"><span data-stu-id="9e710-124">Redis Cache customer query sample</span></span>
<span data-ttu-id="9e710-125">이 샘플은 캐시의 데이터 액세스와 영구적 저장소의 데이터 액세스 간 성능 비교를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span></span> <span data-ttu-id="9e710-126">이 샘플에는 두 개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-126">This sample has two projects.</span></span>

* [<span data-ttu-id="9e710-127">Redis Cache가 데이터를 캐싱하여 성능을 향상시키는 방법 데모</span><span class="sxs-lookup"><span data-stu-id="9e710-127">Demo how Redis Cache can improve performance by Caching data</span></span>](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [<span data-ttu-id="9e710-128">시드는 hello 데모에 대 한 데이터베이스 및 캐시 hello</span><span class="sxs-lookup"><span data-stu-id="9e710-128">Seed hello Database and Cache for hello demo</span></span>](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a><span data-ttu-id="9e710-129">ASP.NET 세션 상태 및 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="9e710-129">ASP.NET Session State and Output Caching</span></span>
<span data-ttu-id="9e710-130">hello [OutputCache 및 SessionState ASP.NET 사용 하 여 Azure Redis Cache toostore](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) 샘플 있습니다 toouse Azure Redis Cache toostore ASP.NET 세션 및 출력 캐시를 사용 하 여 hello에 대 한 공급자 OutputCache 및 SessionState 방법을 보여 줍니다. Redis는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-130">hello [Use Azure Redis Cache toostore ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you toouse Azure Redis Cache toostore ASP.NET Session and Output Cache using hello SessionState and OutputCache providers for Redis.</span></span>

## <a name="manage-azure-redis-cache-with-maml"></a><span data-ttu-id="9e710-131">MAML을 사용하여 Azure Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="9e710-131">Manage Azure Redis Cache with MAML</span></span>
<span data-ttu-id="9e710-132">hello [관리 Azure Redis Cache Azure 관리 라이브러리를 사용 하 여](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 샘플-Azure 관리 라이브러리 toomanage 방법을 사용할 수 있는 방법을 보여 줍니다 (만들기 / 업데이트 / 삭제) 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-132">hello [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries toomanage - (Create/ Update/ delete) your Cache.</span></span> 

## <a name="custom-monitoring-sample"></a><span data-ttu-id="9e710-133">사용자 지정 모니터링 샘플</span><span class="sxs-lookup"><span data-stu-id="9e710-133">Custom monitoring sample</span></span>
<span data-ttu-id="9e710-134">hello [액세스 Redis 캐시 모니터링 데이터](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 샘플 hello Azure 포털 외부에서 Azure Redis Cache에 대 한 모니터링 데이터를 액세스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-134">hello [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of hello Azure Portal.</span></span>

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a><span data-ttu-id="9e710-135">PHP 및 Redis를 사용하여 작성된 Twitter 스타일 클론</span><span class="sxs-lookup"><span data-stu-id="9e710-135">A Twitter-style clone written using PHP and Redis</span></span>
<span data-ttu-id="9e710-136">hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) 샘플은 Redis Hello World hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-136">hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is hello Redis Hello World.</span></span> <span data-ttu-id="9e710-137">Redis 및 hello를 사용 하 여 PHP를 사용 하 여 작성 된 최소한의 Twitter 스타일 소셜 네트워크 복제본 [Predis](https://github.com/nrk/predis) 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-137">It is a minimal Twitter-style social network clone written using Redis and PHP using hello [Predis](https://github.com/nrk/predis) client.</span></span> <span data-ttu-id="9e710-138">hello 소스 코드는 매우 간단한 설계 된 toobe 및 hello에서 동일한 시간 tooshow 다른 Redis 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-138">hello source code is designed toobe very simple and at hello same time tooshow different Redis data structures.</span></span>

## <a name="bandwidth-monitor"></a><span data-ttu-id="9e710-139">대역폭 모니터</span><span class="sxs-lookup"><span data-stu-id="9e710-139">Bandwidth monitor</span></span>
<span data-ttu-id="9e710-140">hello [대역폭 모니터](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) 샘플 hello 클라이언트에서 사용 되는 toomonitor hello 대역폭을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-140">hello [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you toomonitor hello bandwidth used on hello client.</span></span> <span data-ttu-id="9e710-141">toomeasure는 대역폭 hello, hello 샘플 hello 캐시 클라이언트 컴퓨터에서 실행, 호출 toohello 캐시를 확인 및 hello 대역폭 모니터 샘플에서 보고 하는 hello 대역폭을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e710-141">toomeasure hello bandwidth, run hello sample on hello cache client machine, make calls toohello cache, and observe hello bandwidth reported by hello bandwidth monitor sample.</span></span>


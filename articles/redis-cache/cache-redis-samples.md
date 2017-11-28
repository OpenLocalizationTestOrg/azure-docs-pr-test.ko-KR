---
title: "Azure Redis Cache 샘플 | Microsoft Docs"
description: "Azure Redis Cache를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: 7841fcf0b5f4dcb409abf8bfb804c2e03dad6d3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-redis-cache-samples"></a><span data-ttu-id="3b253-103">Azure Redis Cache 샘플</span><span class="sxs-lookup"><span data-stu-id="3b253-103">Azure Redis Cache samples</span></span>
<span data-ttu-id="3b253-104">이 항목에서는 캐시에 연결, 캐시에서 데이터 읽기 및 쓰기, ASP.NET Redis Cache 공급자 사용과 같은 시나리오를 다루는 Azure Redis Cache 샘플 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting to a cache, reading and writing data to and from a cache, and using the ASP.NET Redis Cache providers.</span></span> <span data-ttu-id="3b253-105">일부 샘플은 다운로드 가능한 프로젝트이고, 일부 샘플은 단계별 지침을 제공하며 코드 조각을 포함하지만 다운로드 가능한 프로젝트에 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-105">Some of the samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link to a downloadable project.</span></span>

## <a name="hello-world-samples"></a><span data-ttu-id="3b253-106">Hello world 샘플</span><span class="sxs-lookup"><span data-stu-id="3b253-106">Hello world samples</span></span>
<span data-ttu-id="3b253-107">이 섹션의 샘플은 다양한 언어와 Redis 클라이언트를 사용하여 Azure Redis Cache 인스턴스에 연결하고 캐시에서 데이터를 읽고 쓰는 방법의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-107">The samples in this section show the basics of connecting to an Azure Redis Cache instance and reading and writing data to the cache using a variety of languages and Redis clients.</span></span>

<span data-ttu-id="3b253-108">[Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플에서는 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 클라이언트를 사용하여 다양한 캐시 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-108">The [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how to perform various cache operations using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span></span>

<span data-ttu-id="3b253-109">이 샘플에서는 다음 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-109">This sample shows how to:</span></span>

* <span data-ttu-id="3b253-110">다양한 연결 옵션 사용</span><span class="sxs-lookup"><span data-stu-id="3b253-110">Use various connection options</span></span>
* <span data-ttu-id="3b253-111">동기 및 비동기 작업을 사용하여 캐시에서 개체 읽기 및 캐시에 개체 쓰기</span><span class="sxs-lookup"><span data-stu-id="3b253-111">Read and write objects to and from the cache using synchronous and asynchronous operations</span></span>
* <span data-ttu-id="3b253-112">Redis MGET/MSET 명령을 사용하여 지정된 키 값 반환</span><span class="sxs-lookup"><span data-stu-id="3b253-112">Use Redis MGET/MSET commands to return values of specified keys</span></span>
* <span data-ttu-id="3b253-113">Redis 트랜잭션 작업 수행</span><span class="sxs-lookup"><span data-stu-id="3b253-113">Perform Redis transactional operations</span></span>
* <span data-ttu-id="3b253-114">Redis 목록 및 정렬된 집합 작업</span><span class="sxs-lookup"><span data-stu-id="3b253-114">Work with Redis lists and sorted sets</span></span>
* <span data-ttu-id="3b253-115">JsonConvert serializer를 사용하여.NET 개체 저장</span><span class="sxs-lookup"><span data-stu-id="3b253-115">Store .NET objects using JsonConvert serializers</span></span>
* <span data-ttu-id="3b253-116">Redis 집합을 사용하여 태그 지정 구현</span><span class="sxs-lookup"><span data-stu-id="3b253-116">Use Redis sets to implement tagging</span></span>
* <span data-ttu-id="3b253-117">Redis 클러스터 작업</span><span class="sxs-lookup"><span data-stu-id="3b253-117">Work with Redis Cluster</span></span>

<span data-ttu-id="3b253-118">자세한 내용은 github의 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) 설명서를 참조하세요. 추가 사용 시나리오는 [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) 단위 테스트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b253-118">For more information, see the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see the [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span></span>

<span data-ttu-id="3b253-119">[Azure Redis Cache를 Python과 함께 사용하는 방법](cache-python-get-started.md)에서는 Python과 [redis-py](https://github.com/andymccurdy/redis-py) 클라이언트를 사용하여 Azure Redis Cache를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-119">[How to use Azure Redis Cache with Python](cache-python-get-started.md) shows how to get started with Azure Redis Cache using Python and the [redis-py](https://github.com/andymccurdy/redis-py) client.</span></span>

<span data-ttu-id="3b253-120">[캐시에서 .NET 개체 사용](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) 에서는 Azure Redis Cache 인스턴스에서 읽고 쓸 수 있도록 .NET 개체를 직렬화하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-120">[Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way to serialize .NET objects so you can write them to and read them from an Azure Redis Cache instance.</span></span> 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a><span data-ttu-id="3b253-121">Redis Cache를 ASP.NET SignalR에 대한 규모 확장 백플레인으로 사용</span><span class="sxs-lookup"><span data-stu-id="3b253-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span></span>
<span data-ttu-id="3b253-122">[Redis Cache를 ASP.NET SignalR에 대한 규모 확장 백플레인으로 사용](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) 샘플은 Azure Redis Cache를 SignalR 백플레인으로 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-122">The [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span></span> <span data-ttu-id="3b253-123">백플레인에 대한 자세한 내용은 [Redis를 사용한 SignalR 규모 확장](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b253-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span></span>

## <a name="redis-cache-customer-query-sample"></a><span data-ttu-id="3b253-124">Redis Cache 고객 쿼리 샘플</span><span class="sxs-lookup"><span data-stu-id="3b253-124">Redis Cache customer query sample</span></span>
<span data-ttu-id="3b253-125">이 샘플은 캐시의 데이터 액세스와 영구적 저장소의 데이터 액세스 간 성능 비교를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span></span> <span data-ttu-id="3b253-126">이 샘플에는 두 개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-126">This sample has two projects.</span></span>

* [<span data-ttu-id="3b253-127">Redis Cache가 데이터를 캐싱하여 성능을 향상시키는 방법 데모</span><span class="sxs-lookup"><span data-stu-id="3b253-127">Demo how Redis Cache can improve performance by Caching data</span></span>](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [<span data-ttu-id="3b253-128">데모를 위한 데이터베이스 및 캐시 시드</span><span class="sxs-lookup"><span data-stu-id="3b253-128">Seed the Database and Cache for the demo</span></span>](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a><span data-ttu-id="3b253-129">ASP.NET 세션 상태 및 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="3b253-129">ASP.NET Session State and Output Caching</span></span>
<span data-ttu-id="3b253-130">[Azure Redis Cache를 사용하여 ASP.NET SessionState 및 OutputCache 저장](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) 샘플은 Azure Redis Cache를 사용하여 Redis용 SessionState 및 OutputCache 공급자를 사용하는 ASP.NET 세션 및 출력 캐시를 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-130">The [Use Azure Redis Cache to store ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you to use Azure Redis Cache to store ASP.NET Session and Output Cache using the SessionState and OutputCache providers for Redis.</span></span>

## <a name="manage-azure-redis-cache-with-maml"></a><span data-ttu-id="3b253-131">MAML을 사용하여 Azure Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="3b253-131">Manage Azure Redis Cache with MAML</span></span>
<span data-ttu-id="3b253-132">[Azure Management Libraries를 사용하여 Azure Redis Cache 관리](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 샘플은 Azure Management Libraries를 사용하여 캐시를 관리(만들기/업데이트/삭제)하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-132">The [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries to manage - (Create/ Update/ delete) your Cache.</span></span> 

## <a name="custom-monitoring-sample"></a><span data-ttu-id="3b253-133">사용자 지정 모니터링 샘플</span><span class="sxs-lookup"><span data-stu-id="3b253-133">Custom monitoring sample</span></span>
<span data-ttu-id="3b253-134">[Redis Cache 모니터링 데이터 액세스](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 샘플은 Azure 포털 외부에서 Azure Redis Cache에 대한 모니터링 데이터에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-134">The [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of the Azure Portal.</span></span>

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a><span data-ttu-id="3b253-135">PHP 및 Redis를 사용하여 작성된 Twitter 스타일 클론</span><span class="sxs-lookup"><span data-stu-id="3b253-135">A Twitter-style clone written using PHP and Redis</span></span>
<span data-ttu-id="3b253-136">[Retwis](https://github.com/SyntaxC4-MSFT/retwis) 샘플은 Redis Hello World입니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-136">The [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is the Redis Hello World.</span></span> <span data-ttu-id="3b253-137">Redis 및 PHP를 사용하여 작성된 최소 Twitter 스타일 소셜 네트워크 클론으로, [Predis](https://github.com/nrk/predis) 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-137">It is a minimal Twitter-style social network clone written using Redis and PHP using the [Predis](https://github.com/nrk/predis) client.</span></span> <span data-ttu-id="3b253-138">소스 코드는 매우 간단하며 동시에 서로 다른 Redis 데이터 구조를 보여주도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-138">The source code is designed to be very simple and at the same time to show different Redis data structures.</span></span>

## <a name="bandwidth-monitor"></a><span data-ttu-id="3b253-139">대역폭 모니터</span><span class="sxs-lookup"><span data-stu-id="3b253-139">Bandwidth monitor</span></span>
<span data-ttu-id="3b253-140">[대역폭 모니터](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) 샘플을 사용하면 클라이언트에서 사용 되는 대역폭을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-140">The [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you to monitor the bandwidth used on the client.</span></span> <span data-ttu-id="3b253-141">대역폭을 측정하려면 캐시 클라이언트 컴퓨터에서 샘플을 실행하고, 캐시를 호출하고, 대역폭 모니터 샘플에서 보고하는 대역폭을 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="3b253-141">To measure the bandwidth, run the sample on the cache client machine, make calls to the cache, and observe the bandwidth reported by the bandwidth monitor sample.</span></span>


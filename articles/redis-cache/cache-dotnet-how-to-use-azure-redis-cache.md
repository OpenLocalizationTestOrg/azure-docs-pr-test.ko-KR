---
title: Azure Redis Cache aaaHow tooUse | Microsoft Docs
description: "Tooimprove Azure Redis 캐시와 Azure 응용 프로그램의 성능을 hello 하는 방법에 대해 알아봅니다"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="d5c94-103">Azure Redis 캐시 하는 tooUse 방법</span><span class="sxs-lookup"><span data-stu-id="d5c94-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5c94-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d5c94-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="d5c94-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d5c94-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="d5c94-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d5c94-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="d5c94-107">Java</span><span class="sxs-lookup"><span data-stu-id="d5c94-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="d5c94-108">Python</span><span class="sxs-lookup"><span data-stu-id="d5c94-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="d5c94-109">이 가이드에서는 알아봅니다 tooget를 사용 하 여 시작 방법을 **Azure Redis Cache**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="d5c94-110">Microsoft Azure Redis Cache hello 인기 있는 오픈 소스 Redis Cache를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="d5c94-111">제공 tooa 안전한 전용된 Redis 캐시, Microsoft에서 관리 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="d5c94-112">Azure Redis 캐시를 사용하여 만들어진 캐시는 Microsoft Azure 내의 모든 응용 프로그램에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="d5c94-113">Microsoft Azure Redis Cache는 hello 다음 계층에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="d5c94-114">**기본** – 단일 노드.</span><span class="sxs-lookup"><span data-stu-id="d5c94-114">**Basic** – Single node.</span></span> <span data-ttu-id="d5c94-115">Too53 GB 여러 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="d5c94-116">**표준** – 2노드 주/복제본.</span><span class="sxs-lookup"><span data-stu-id="d5c94-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="d5c94-117">Too53 GB 여러 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="d5c94-118">99.9% SLA</span><span class="sxs-lookup"><span data-stu-id="d5c94-118">99.9% SLA.</span></span>
* <span data-ttu-id="d5c94-119">**프리미엄** – 두 노드 주/복제본와 시작 too10 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="d5c94-120">GB too530 6GB 여러 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="d5c94-121">모든 표준 계층 기능과 추가적인 [Redis 클러스터](cache-how-to-premium-clustering.md), [Redis 지속성](cache-how-to-premium-persistence.md) 및 [Azure Virtual Network](cache-how-to-premium-vnet.md) 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="d5c94-122">99.9% SLA</span><span class="sxs-lookup"><span data-stu-id="d5c94-122">99.9% SLA.</span></span>

<span data-ttu-id="d5c94-123">각 계층은 기능과 가격이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="d5c94-124">가격 책정에 대한 내용은 [캐시 가격 책정 정보][Cache Pricing Details]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c94-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="d5c94-125">이 가이드에서는 toouse hello [StackExchange.Redis] [ StackExchange.Redis] C를 사용 하 여 클라이언트\# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="d5c94-126">hello 가이드에서 다루는 시나리오 포함 **만들기 및 구성 캐시**, **캐시 클라이언트 구성**, 및 **추가 하 고 hello 캐시에서 개체 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="d5c94-127">Azure Redis Cache 사용에 대한 자세한 내용은 [다음 단계][Next Steps]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c94-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="d5c94-128">ASP.NET MVC Redis 캐시와 웹 응용 프로그램 빌드 과정의 단계별 자습서를 참조 하십시오. [어떻게 toocreate Redis Cache에 웹 앱](cache-web-app-howto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="d5c94-129">Azure Redis Cache 시작</span><span class="sxs-lookup"><span data-stu-id="d5c94-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="d5c94-130">Azure Redis 캐시를 시작하기는 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="d5c94-131">tooget 하면 프로 비전을 시작 하 고 캐시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="d5c94-132">다음으로 hello 캐시 액세스할 수 있도록 hello 캐시 클라이언트 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="d5c94-133">Hello 캐시 클라이언트를 구성한 후 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="d5c94-134">[Hello 캐시 만들기][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="d5c94-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="d5c94-135">[Hello 캐시 클라이언트 구성][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="d5c94-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="d5c94-136">캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="d5c94-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="d5c94-137">tooaccess 그 뒤에 캐시는 생성</span><span class="sxs-lookup"><span data-stu-id="d5c94-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="d5c94-138">캐시를 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconfigure Azure Redis Cache](cache-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="d5c94-139">Hello 캐시 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="d5c94-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="d5c94-140">캐싱에 대 한 클라이언트 프로젝트 구성 되 면 hello 다음 캐시 작업에 대 한 섹션에에서 설명 된 hello 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="d5c94-141">캐시 작업</span><span class="sxs-lookup"><span data-stu-id="d5c94-141">Working with Caches</span></span>
<span data-ttu-id="d5c94-142">이 섹션의 hello 단계 tooperform 일반 캐시와 작업 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="d5c94-143">[Toohello 캐시를 연결 합니다.][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="d5c94-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="d5c94-144">[추가 하 고 hello 캐시에서 개체를 검색 합니다.][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="d5c94-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="d5c94-145">Hello 캐시에서.NET 개체 사용</span><span class="sxs-lookup"><span data-stu-id="d5c94-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="d5c94-146">Toohello 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-146">Connect toohello cache</span></span>
<span data-ttu-id="d5c94-147">tooprogrammatically 작업 참조 toohello 캐시는 캐시를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="d5c94-148">Hello toohello 위쪽 원하는 toouse hello StackExchange.Redis 클라이언트 tooaccess Azure Redis Cache 모든 파일의 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="d5c94-149">hello StackExchange.Redis 클라이언트에.NET Framework 4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="d5c94-150">Azure Redis Cache hello에서 관리 하는 연결 toohello hello `ConnectionMultiplexer` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="d5c94-151">이 클래스는 공유 되지 않아야 하 고 클라이언트 응용 프로그램 전반에 걸쳐 다시 하며 toobe 작업 별로 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="d5c94-152">tooconnect tooan Azure Redis Cache의 연결 된 인스턴스를 반환 될 `ConnectionMultiplexer`, 정적 호출 hello `Connect` 메서드와 hello 전달 캐시 끝점 및 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="d5c94-153">Hello hello password 매개 변수도 Azure 포털에서에서 생성 된 hello 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="d5c94-154">경고: 소스 코드에 자격 증명을 저장해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="d5c94-155">tookeep이 샘플 단순 하 고 여기서 설명으로 hello 소스 코드에서.</span><span class="sxs-lookup"><span data-stu-id="d5c94-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="d5c94-156">참조 [방법을 응용 프로그램 문자열 및 연결 문자열 작업] [ How Application Strings and Connection Strings Work] 방법에 대 한 내용은 toostore 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="d5c94-157">SSL toouse 않으려면 설정 하거나 `ssl=false` hello를 생략 하거나 `ssl` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="d5c94-158">hello 비 SSL 포트는 새 캐시에 대해 기본적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="d5c94-159">Hello 비 SSL 포트를 사용 하도록 설정 하면 지침은 [액세스 포트](cache-configure.md#access-ports)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="d5c94-160">한 가지 방법은 toosharing는 `ConnectionMultiplexer` 응용 프로그램에서 인스턴스가 toohave 비슷한 toohello 다음 예제에서는 연결 된 인스턴스를 반환 하는 정적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="d5c94-161">이 방법은 제공 스레드로부터 안전한 방식으로 tooinitialize 연결 하나만 `ConnectionMultiplexer` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="d5c94-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="d5c94-162">다음 예에서 `abortConnect` hello 호출이 연결 toohello Azure Redis Cache 설정 되지 않으며 경우에 성공 하는 집합 toofalse 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="d5c94-163">주요 기능 중 하나 `ConnectionMultiplexer` 는 자동으로 복원 연결 toohello 캐시 hello 네트워크 문제 또는 다른 원인이 해결 되 면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="d5c94-164">고급 연결 구성 옵션에 대한 자세한 내용은 [StackExchange.Redis 구성 모델][StackExchange.Redis configuration model](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c94-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="d5c94-165">Hello 연결이 설정 되 면 별 참조 toohello redis cache 데이터베이스 호출 hello `ConnectionMultiplexer.GetDatabase` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d5c94-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="d5c94-166">hello에서 반환 된 hello 개체 `GetDatabase` 메서드 경량의 통과 개체 이며 저장 toobe 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="d5c94-167">Azure Redis cache Redis 캐시 내에서 사용 되는 toologically 별도 hello 데이터 일 수 있는 (기본값 16) 데이터베이스의 구성 가능한 번호가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="d5c94-168">자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases) 및 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c94-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="d5c94-169">Tooconnect tooan Azure Redis Cache 인스턴스 및 참조 toohello 반환 데이터베이스에서 캐시 방법을 파악 했으므로 hello 캐시 작업에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="d5c94-170">추가 하 고 hello 캐시에서 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="d5c94-171">항목에 저장 하 고 hello를 사용 하 여 캐시에서 검색할 수 `StringSet` 및 `StringGet` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d5c94-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="d5c94-172">Redis 저장소 Redis 문자열 하지만 이러한 문자열 대부분의 데이터에는 다양 한 유형의 hello 캐시에 개체를.NET 저장할 때 사용할 수 있는 serialize 된 이진 데이터를 포함 한 데이터를 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="d5c94-173">호출할 때 `StringGet`, hello 개체가 있는 경우 반환 되는, 존재 하지 않는 경우 `null` 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="d5c94-174">경우 `null` 반환 되 면 hello 원하는 데이터 원본에서 hello 값을 검색 하 및 이후 사용에 대 한 hello 캐시에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="d5c94-175">이 사용 패턴 hello 캐시 배제 패턴 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="d5c94-176">사용할 수도 있습니다 `RedisValue`hello 다음 예제에에서 나온 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="d5c94-177">`RedisValue`는 정수 데이터 형식을 작업하기 위한 암시적 연산자를 갖고 있으며, 캐시된 항목의 값으로 `null`이 예상되는 경우에 유용하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="d5c94-178">hello 캐시를 사용 하 여 hello에 있는 항목의 toospecify hello 만료 `TimeSpan` 의 매개 변수 `StringSet`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="d5c94-179">Hello 캐시에서.NET 개체 사용</span><span class="sxs-lookup"><span data-stu-id="d5c94-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="d5c94-180">Azure Redis Cache는 .NET 개체 및 기본 데이터 유형을 캐시할 수 있지만 .NET 개체를 캐시하려면 먼저 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="d5c94-181">이.NET 개체 serialization hello 응용 프로그램 개발자의 책임 hello 있으며 hello serializer의 hello 선택에 hello 개발자 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="d5c94-182">하나의 간단한 방법을 tooserialize 개체는 toouse hello `JsonConvert` 의 serialization 메서드 [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) JSON에서 tooand serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="d5c94-183">hello 다음 보여 주는 예제는 get 및 set를 사용 하는 `Employee` 개체 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="d5c94-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5c94-184">Next Steps</span></span>
<span data-ttu-id="d5c94-185">Hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure Redis Cache에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="d5c94-186">체크 아웃 hello Azure Redis Cache 용 ASP.NET 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="d5c94-187">Azure Redis 세션 상태 공급자</span><span class="sxs-lookup"><span data-stu-id="d5c94-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="d5c94-188">Azure Redis Cache ASP.NET 출력 캐시 공급자</span><span class="sxs-lookup"><span data-stu-id="d5c94-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="d5c94-189">[캐시 진단을 사용 하도록 설정](cache-how-to-monitor.md#enable-cache-diagnostics) 할 수 있도록 [모니터](cache-how-to-monitor.md) hello 캐시의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="d5c94-190">Hello 수도 hello Azure 포털에서 메트릭을 볼 수 있습니다 [다운로드 하 여 검토](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 선택한 hello 도구를 사용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="d5c94-191">체크 아웃 hello [StackExchange.Redis 캐시 클라이언트 설명서][StackExchange.Redis cache client documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="d5c94-192">Azure Redis Cache는 다양한 Redis 클라이언트와 개발 언어에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="d5c94-193">자세한 내용은 [http://redis.io/clients][http://redis.io/clients]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5c94-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="d5c94-194">Redsmin 및 Redis Desktop Manager와 같은 타사 서비스 및 도구와 함께 Azure Redis Cache를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="d5c94-195">Redsmin에 대 한 자세한 내용은 참조 [어떻게 tooretrieve Azure Redis 연결 문자열을 사용 하 여 Redsmin와][How tooretrieve an Azure Redis connection string and use it with Redsmin]합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="d5c94-196">[RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)를 사용하여 GUI가 포함된 Azure Redis Cache의 데이터에 액세스하고 해당 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="d5c94-197">Hello 참조 [redis] [ redis] 설명서 및 읽기에 대 한 [redis 데이터 형식을] [ redis data types] 및 [15 분 소개 데이터 형식 tooRedis][a fifteen minute introduction tooRedis data types]합니다.</span><span class="sxs-lookup"><span data-stu-id="d5c94-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/



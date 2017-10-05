---
title: "Azure Redis Cache를 사용하는 방법 | Microsoft 문서"
description: "Azure Redis Cache를 사용하여 Azure 응용 프로그램의 성능을 향상시키는 방법을 알아봅니다."
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="83e5d-103">Azure Redis Cache 사용 방법</span><span class="sxs-lookup"><span data-stu-id="83e5d-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83e5d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="83e5d-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="83e5d-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="83e5d-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="83e5d-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="83e5d-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="83e5d-107">Java</span><span class="sxs-lookup"><span data-stu-id="83e5d-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="83e5d-108">Python</span><span class="sxs-lookup"><span data-stu-id="83e5d-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="83e5d-109">이 가이드에서는 **Azure Redis Cache**를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="83e5d-110">Microsoft Azure Redis Cache는 많이 사용되는 오픈 소스 Redis Cache를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="83e5d-111">Microsoft에서 관리하는 안전한 전용 Redis Cache에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="83e5d-112">Azure Redis 캐시를 사용하여 만들어진 캐시는 Microsoft Azure 내의 모든 응용 프로그램에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="83e5d-113">Microsoft Azure Redis 캐시는 다음 계층에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="83e5d-114">**기본** – 단일 노드.</span><span class="sxs-lookup"><span data-stu-id="83e5d-114">**Basic** – Single node.</span></span> <span data-ttu-id="83e5d-115">최대 53GB까지 여러 개의 크기</span><span class="sxs-lookup"><span data-stu-id="83e5d-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="83e5d-116">**표준** – 2노드 주/복제본.</span><span class="sxs-lookup"><span data-stu-id="83e5d-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="83e5d-117">최대 53GB까지 여러 개의 크기</span><span class="sxs-lookup"><span data-stu-id="83e5d-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="83e5d-118">99.9% SLA</span><span class="sxs-lookup"><span data-stu-id="83e5d-118">99.9% SLA.</span></span>
* <span data-ttu-id="83e5d-119">**프리미엄** – 최대 10개 분할 데이터베이스와 2노드 주/복제본.</span><span class="sxs-lookup"><span data-stu-id="83e5d-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="83e5d-120">6GB ~ 530GB에 이르는 여러 개의 크기</span><span class="sxs-lookup"><span data-stu-id="83e5d-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="83e5d-121">모든 표준 계층 기능과 추가적인 [Redis 클러스터](cache-how-to-premium-clustering.md), [Redis 지속성](cache-how-to-premium-persistence.md) 및 [Azure Virtual Network](cache-how-to-premium-vnet.md) 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="83e5d-122">99.9% SLA</span><span class="sxs-lookup"><span data-stu-id="83e5d-122">99.9% SLA.</span></span>

<span data-ttu-id="83e5d-123">각 계층은 기능과 가격이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="83e5d-124">가격 책정에 대한 내용은 [캐시 가격 책정 정보][Cache Pricing Details]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="83e5d-125">이 가이드는 C\# 코드를 사용하는 [StackExchange.Redis][StackExchange.Redis] 클라이언트 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="83e5d-126">적용되는 시나리오에는 **캐시 만들기 및 구성**, **캐시 클라이언트 구성** 및 **캐시에서 개체 추가 및 제거** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="83e5d-127">Azure Redis Cache 사용에 대한 자세한 내용은 [다음 단계][Next Steps]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="83e5d-128">Redis Cache를 사용하여 ASP.NET MVC 웹앱을 만드는 단계별 자습서는 [Redis Cache를 사용하여 웹앱을 만드는 방법](cache-web-app-howto.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="83e5d-129">Azure Redis Cache 시작</span><span class="sxs-lookup"><span data-stu-id="83e5d-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="83e5d-130">Azure Redis 캐시를 시작하기는 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="83e5d-131">먼저 캐시를 프로비전하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="83e5d-132">그런 다음 캐시에 액세스할 수 있도록 캐시 클라이언트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="83e5d-133">캐시 클라이언트를 구성하면 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="83e5d-134">[캐시 만들기][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="83e5d-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="83e5d-135">[캐시 클라이언트 구성][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="83e5d-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="83e5d-136">캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="83e5d-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="83e5d-137">캐시를 만든 후 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="83e5d-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="83e5d-138">캐시 구성에 대한 자세한 내용은 [Azure Redis Cache를 구성하는 방법을](cache-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="83e5d-139">캐시 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="83e5d-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="83e5d-140">클라이언트 프로젝트의 캐싱을 구성했으면 캐시 작업에 대해 다음 섹션에서 설명하는 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="83e5d-141">캐시 작업</span><span class="sxs-lookup"><span data-stu-id="83e5d-141">Working with Caches</span></span>
<span data-ttu-id="83e5d-142">이 섹션의 각 단계에서는 일반적인 캐시 작업 수행 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="83e5d-143">[캐시에 연결][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="83e5d-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="83e5d-144">[캐시에서 개체 추가 및 검색][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="83e5d-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="83e5d-145">캐시의 .NET 개체 사용</span><span class="sxs-lookup"><span data-stu-id="83e5d-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="83e5d-146">캐시에 연결</span><span class="sxs-lookup"><span data-stu-id="83e5d-146">Connect to the cache</span></span>
<span data-ttu-id="83e5d-147">프로그래밍 방식으로 캐시 작업을 하려면 캐시에 대한 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="83e5d-148">StackExchange.Redis 클라이언트를 사용하여 Azure Redis Cache에 액세스하는 위치가 되는 임의의 파일 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="83e5d-149">StackExchange.Redis 클라이언트를 사용하려면 .NET Framework 4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="83e5d-150">Azure Redis Cache 연결은 `ConnectionMultiplexer` 클래스로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="83e5d-151">이 클래스는 클라이언트 응용 프로그램 전체에서 공유되고 다시 사용되어야 하며 작업별로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="83e5d-152">Azure Redis Cache에 연결하고 연결된 `ConnectionMultiplexer` 인스턴스가 반환되도록 하려면 정적 `Connect` 메서드를 호출하여 캐시 끝점 및 키에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="83e5d-153">Azure Portal에서 생성된 키를 암호 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="83e5d-154">경고: 소스 코드에 자격 증명을 저장해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="83e5d-155">이 샘플을 단순하게 유지하기 위해 소스 코드로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="83e5d-156">[응용 프로그램 설정 및 연결 문자열 작동 방식][How Application Strings and Connection Strings Work](영문)에서 자격 증명 저장 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="83e5d-157">SSL을 사용하지 않으려면 `ssl=false`를 설정하거나 `ssl` 매개 변수를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="83e5d-158">비 SSL 포트는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="83e5d-159">비 SSL 포트를 사용하도록 설정하는 지침은 [포트 액세스](cache-configure.md#access-ports)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="83e5d-160">응용 프로그램의 `ConnectionMultiplexer` 인스턴스를 공유하는 방법은 다음 예제와 비슷하게 연결된 인스턴스를 반환하는 정적 속성을 갖는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="83e5d-161">이 방법은 스레드가 안전하도록 단일 연결된 `ConnectionMultiplexer` 인스턴스를 초기화하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="83e5d-162">이 예에서 `abortConnect`는 false로 설정되며 이것은 Azure Redis Cache에 연결이 설정되지 않은 경우에도 호출이 성공한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="83e5d-163">`ConnectionMultiplexer`의 한 가지 주요 기능은 네트워크 문제 또는 다른 원인이 해결되면 캐시에 연결이 자동으로 복원된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="83e5d-164">고급 연결 구성 옵션에 대한 자세한 내용은 [StackExchange.Redis 구성 모델][StackExchange.Redis configuration model](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="83e5d-165">연결이 설정되고 나면 `ConnectionMultiplexer.GetDatabase` 메서드를 호출하여 Redis Cache 데이터베이스에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="83e5d-166">`GetDatabase` 메서드에서 반환된 개체는 경량의 통과 개체이며 저장할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="83e5d-167">Azure Redis Cache에는 Redis 캐시 내에서 데이터를 논리적으로 구분하는 데 사용할 수 있는 여러 개의 구성 가능한 데이터베이스(기본 16개)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="83e5d-168">자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases) 및 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="83e5d-169">Azure Redis Cache 인스턴스에 연결하고 캐시 데이터베이스에 대한 참조를 반환하는 방법을 알아보았으며, 이제 캐시 작업에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="83e5d-170">캐시에서 개체 추가 및 검색</span><span class="sxs-lookup"><span data-stu-id="83e5d-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="83e5d-171">`StringSet` 및 `StringGet` 메서드를 사용하여 캐시에 항목을 저장하고 캐시에서 항목을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="83e5d-172">Redis는 대부분의 데이터를 Redis 문자열로 저장하지만, 이 문자열은 캐시에 .NET 개체를 저장할 때 사용할 수 있는 직렬화된 이진 데이터를 포함하여 다양한 데이터 유형을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="83e5d-173">`StringGet` 호출 시 개체가 있으면 반환되고 없으면 `null`이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="83e5d-174">`null`이 반환되면 원하는 데이터 원본에서 값을 검색하여 이후에 사용할 수 있게 캐시에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="83e5d-175">이런 사용 패턴을 캐시 배제 패턴이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="83e5d-176">다음 예제에 나온 것처럼 `RedisValue`를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="83e5d-177">`RedisValue`는 정수 데이터 형식을 작업하기 위한 암시적 연산자를 갖고 있으며, 캐시된 항목의 값으로 `null`이 예상되는 경우에 유용하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="83e5d-178">캐시에서 항목의 만료를 지정하려면 `StringSet`의 `TimeSpan` 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="83e5d-179">캐시의 .NET 개체 사용</span><span class="sxs-lookup"><span data-stu-id="83e5d-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="83e5d-180">Azure Redis Cache는 .NET 개체 및 기본 데이터 유형을 캐시할 수 있지만 .NET 개체를 캐시하려면 먼저 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="83e5d-181">.NET 개체 직렬화는 응용 프로그램 개발자의 책임이며 개발자는 유연하게 직렬 변환기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="83e5d-182">개체를 직렬화하는 간단한 방법은 [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1)에서 `JsonConvert` 직렬화 방법을 사용하고 JSON 간에 직렬화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="83e5d-183">다음 예제에서는 `Employee` 개체 인스턴스를 사용하는 가져오기 및 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="83e5d-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83e5d-184">Next Steps</span></span>
<span data-ttu-id="83e5d-185">이제 기본 사항을 배웠으므로 다음 링크를 따라 Azure Redis Cache에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="83e5d-186">Azure Redis Cache에 대한 ASP.NET 공급자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="83e5d-187">Azure Redis 세션 상태 공급자</span><span class="sxs-lookup"><span data-stu-id="83e5d-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="83e5d-188">Azure Redis Cache ASP.NET 출력 캐시 공급자</span><span class="sxs-lookup"><span data-stu-id="83e5d-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="83e5d-189">[캐시 진단을 사용](cache-how-to-monitor.md#enable-cache-diagnostics)하도록 설정하면 캐시의 상태를 [모니터링](cache-how-to-monitor.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="83e5d-190">Azure Portal에서 메트릭을 볼 수 있으며 선택한 도구를 사용하여 메트릭을 [다운로드 및 검토](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="83e5d-191">[StackExchange.Redis 캐시 클라이언트 설명서][StackExchange.Redis cache client documentation](영문)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="83e5d-192">Azure Redis Cache는 다양한 Redis 클라이언트와 개발 언어에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="83e5d-193">자세한 내용은 [http://redis.io/clients][http://redis.io/clients]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="83e5d-194">Redsmin 및 Redis Desktop Manager와 같은 타사 서비스 및 도구와 함께 Azure Redis Cache를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="83e5d-195">Redsmin에 대한 자세한 내용은 [Azure Redis 연결 문자열을 검색하고 Redsmin과 함께 사용하는 방법][How to retrieve an Azure Redis connection string and use it with Redsmin]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="83e5d-196">[RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)를 사용하여 GUI가 포함된 Azure Redis Cache의 데이터에 액세스하고 해당 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="83e5d-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="83e5d-197">[redis][redis](영문) 설명서를 참조하고 [redis 데이터 형식][redis data types](영문) 및 [Redis 데이터 형식에 대한 15분 소개][a fifteen minute introduction to Redis data types](영문)에 대해 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="83e5d-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/



---
title: "aaaHow toouse Java와 함께 Azure Redis Cache | Microsoft Docs"
description: "Java를 사용하여 Azure Redis Cache를 시작합니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="3072f-103">Toouse Azure Redis 캐시 방법 Java와 함께</span><span class="sxs-lookup"><span data-stu-id="3072f-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3072f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3072f-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="3072f-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3072f-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="3072f-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3072f-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="3072f-107">Java</span><span class="sxs-lookup"><span data-stu-id="3072f-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="3072f-108">Python</span><span class="sxs-lookup"><span data-stu-id="3072f-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="3072f-109">Azure Redis Cache 액세스할 수 있도록 tooa 전용된 Redis 캐시를 Microsoft에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="3072f-110">Microsoft Azure 내의 모든 응용 프로그램에서 캐시에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="3072f-111">이 항목에서는 tooget Azure Redis Cache를 어떻게 시작 Java를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3072f-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3072f-112">Prerequisites</span></span>
<span data-ttu-id="3072f-113">[Jedis](https://github.com/xetorthio/jedis) - Redis용 Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3072f-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="3072f-114">이 자습서에서는 Jedis를 사용하지만 [http://redis.io/clients](http://redis.io/clients)에 나열된 모든 Java 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="3072f-115">Azure에 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="3072f-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="3072f-116">Hello 호스트 이름 및 액세스 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="3072f-117">SSL을 통해 안전 하 게 toohello 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="3072f-118">최신 빌드를 hello [jedis](https://github.com/xetorthio/jedis) tooAzure Redis Cache를 연결 하기 위한 지원을 제공 SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="3072f-119">다음 예제는 hello tooconnect tooAzure Redis Cache를 사용 하 여 6380의 SSL 끝점을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="3072f-120">대체 `<name>` 캐시 hello 이름의 및 `<key>` 사용 하 여 기본 또는 보조 키에 설명 된 대로 hello 이전 [hello 호스트 이름 및 액세스 키를 검색](#retrieve-the-host-name-and-access-keys) 섹션.</span><span class="sxs-lookup"><span data-stu-id="3072f-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="3072f-121">새 Azure Redis 캐시 인스턴스에 대 한 hello 비 SSL 포트를 사용 하는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="3072f-122">SSL을 지원 하지 않는 다른 클라이언트를 사용 하는 경우 참조 [어떻게 tooenable hello 비 SSL 포트](cache-configure.md#access-ports)합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="3072f-123">추가 toohello을 캐시 하 고 검색</span><span class="sxs-lookup"><span data-stu-id="3072f-123">Add something toohello cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="3072f-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3072f-124">Next steps</span></span>
* <span data-ttu-id="3072f-125">[캐시 진단을 사용 하도록 설정](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) 할 수 있도록 [모니터](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello 캐시의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="3072f-126">읽기 hello 공식 [설명서 Redis](http://redis.io/documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="3072f-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

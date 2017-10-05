---
title: "Azure Redis Cache를 Node.js와 함께 사용하는 방법 | Microsoft 문서"
description: "Node.js 및 node_redis를 사용하여 Azure Redis Cache를 시작합니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="a3767-103">Azure Redis Cache를 Node.js와 함께 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="a3767-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3767-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a3767-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="a3767-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a3767-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="a3767-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a3767-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="a3767-107">Java</span><span class="sxs-lookup"><span data-stu-id="a3767-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="a3767-108">Python</span><span class="sxs-lookup"><span data-stu-id="a3767-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="a3767-109">Azure Redis Cache는 Microsoft에서 관리하는 안전한 전용 Redis Cache에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="a3767-110">Microsoft Azure 내의 모든 응용 프로그램에서 캐시에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="a3767-111">이 항목에서는 Node.js를 사용하여 Azure Redis Cache를 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="a3767-112">Azure Redis Cache를 Node.js와 함께 사용하는 방법에 대한 다른 예는 [Azure 웹 사이트에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드](../app-service-web/web-sites-nodejs-chat-app-socketio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3767-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3767-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a3767-113">Prerequisites</span></span>
<span data-ttu-id="a3767-114">[node_redis](https://github.com/mranney/node_redis) 설치:</span><span class="sxs-lookup"><span data-stu-id="a3767-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="a3767-115">이 자습서에서는 [node_redis](https://github.com/mranney/node_redis)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="a3767-116">다른 Node.js 클라이언트를 사용한 예는 [Node.js Redis 클라이언트](http://redis.io/clients#nodejs)에 나열된 Node.js 클라이언트의 개별 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3767-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="a3767-117">Azure에 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="a3767-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="a3767-118">호스트 이름 및 액세스 키 검색</span><span class="sxs-lookup"><span data-stu-id="a3767-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="a3767-119">SSL을 사용하여 안전하게 캐시에 연결</span><span class="sxs-lookup"><span data-stu-id="a3767-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="a3767-120">[node_redis](https://github.com/mranney/node_redis)의 최신 빌드는 SSL을 사용하여 Azure Redis Cache에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="a3767-121">다음 예제에서는 6380 SSL 끝점을 사용하여 Azure Redis Cache에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="a3767-122">이전의 [호스트 이름 및 액세스 키 검색](#retrieve-the-host-name-and-access-keys) 섹션에서 설명된 대로 `<name>`을(를) 캐시의 이름으로 `<key>`을(를) 기본 또는 보조 키로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="a3767-123">비 SSL 포트는 새 Azure Redis Cache 인스턴스에 대해 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="a3767-124">SSL을 지원하지 않는 다른 클라이언트를 사용하는 경우 [비 SSL 포트를 사용하도록 설정하는 방법](cache-configure.md#access-ports)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3767-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="a3767-125">캐시에 항목 추가 및 검색</span><span class="sxs-lookup"><span data-stu-id="a3767-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="a3767-126">다음 예제에서는 Azure Redis Cache 인스턴스에 연결하여 캐시의 항목을 저장하고 검색하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="a3767-127">[node_redis](https://github.com/mranney/node_redis) 클라이언트가 포함된 Redis 사용에 관한 더 많은 예는 [http://redis.js.org/](http://redis.js.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3767-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="a3767-128">출력:</span><span class="sxs-lookup"><span data-stu-id="a3767-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="a3767-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3767-129">Next steps</span></span>
* <span data-ttu-id="a3767-130">[캐시 진단을 사용](cache-how-to-monitor.md#enable-cache-diagnostics)하도록 설정하면 캐시의 상태를 [모니터링](cache-how-to-monitor.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3767-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="a3767-131">공식 [Redis 설명서](http://redis.io/documentation)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a3767-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>


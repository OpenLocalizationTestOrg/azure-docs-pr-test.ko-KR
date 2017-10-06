---
title: "Node.js와 함께 Azure Redis Cache aaaHow toouse | Microsoft Docs"
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
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="07ac0-103">Toouse Azure Redis 캐시 방법 Node.js와 함께</span><span class="sxs-lookup"><span data-stu-id="07ac0-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07ac0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="07ac0-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="07ac0-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="07ac0-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="07ac0-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="07ac0-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="07ac0-107">Java</span><span class="sxs-lookup"><span data-stu-id="07ac0-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="07ac0-108">Python</span><span class="sxs-lookup"><span data-stu-id="07ac0-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="07ac0-109">Azure Redis 캐시 제공 tooa 안전한 전용된 Redis 캐시, Microsoft에서 관리 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="07ac0-110">Microsoft Azure 내의 모든 응용 프로그램에서 캐시에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="07ac0-111">이 항목에서는 tooget Azure Redis Cache를 어떻게 시작 Node.js를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="07ac0-112">Azure Redis Cache를 Node.js와 함께 사용하는 방법에 대한 다른 예는 [Azure 웹 사이트에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드](../app-service-web/web-sites-nodejs-chat-app-socketio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07ac0-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07ac0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="07ac0-113">Prerequisites</span></span>
<span data-ttu-id="07ac0-114">[node_redis](https://github.com/mranney/node_redis) 설치:</span><span class="sxs-lookup"><span data-stu-id="07ac0-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="07ac0-115">이 자습서에서는 [node_redis](https://github.com/mranney/node_redis)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="07ac0-116">다른 Node.js 클라이언트를 사용 하 여의 예에 나열 된 hello Node.js 클라이언트에 대 한 hello 개별 설명서를 참조 [Node.js Redis 클라이언트](http://redis.io/clients#nodejs)합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="07ac0-117">Azure에 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="07ac0-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="07ac0-118">Hello 호스트 이름 및 액세스 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="07ac0-119">SSL을 통해 안전 하 게 toohello 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="07ac0-120">최신 빌드를 hello [node_redis](https://github.com/mranney/node_redis) tooAzure Redis Cache를 연결 하기 위한 지원을 제공 SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="07ac0-121">다음 예제는 hello tooconnect tooAzure Redis Cache를 사용 하 여 6380의 SSL 끝점을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="07ac0-122">대체 `<name>` 캐시 hello 이름의 및 `<key>` 사용 하 여 기본 또는 보조 키에 설명 된 대로 hello 이전 [hello 호스트 이름 및 액세스 키를 검색](#retrieve-the-host-name-and-access-keys) 섹션.</span><span class="sxs-lookup"><span data-stu-id="07ac0-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="07ac0-123">새 Azure Redis 캐시 인스턴스에 대 한 hello 비 SSL 포트를 사용 하는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="07ac0-124">SSL을 지원 하지 않는 다른 클라이언트를 사용 하는 경우 참조 [어떻게 tooenable hello 비 SSL 포트](cache-configure.md#access-ports)합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="07ac0-125">추가 toohello을 캐시 하 고 검색</span><span class="sxs-lookup"><span data-stu-id="07ac0-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="07ac0-126">다음 예제와 있습니다 tooconnect tooan Azure Redis 캐시 인스턴스를 하 고 저장 하는 방법과 hello 캐시에서 항목을 검색 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="07ac0-127">Redis를 사용 하 여 hello로의 추가 예 [node_redis](https://github.com/mranney/node_redis) 클라이언트 참조 [http://redis.js.org/](http://redis.js.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="07ac0-128">출력:</span><span class="sxs-lookup"><span data-stu-id="07ac0-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="07ac0-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07ac0-129">Next steps</span></span>
* <span data-ttu-id="07ac0-130">[캐시 진단을 사용 하도록 설정](cache-how-to-monitor.md#enable-cache-diagnostics) 할 수 있도록 [모니터](cache-how-to-monitor.md) hello 캐시의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="07ac0-131">읽기 hello 공식 [설명서 Redis](http://redis.io/documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="07ac0-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>


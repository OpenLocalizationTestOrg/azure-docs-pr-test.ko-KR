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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Toouse Azure Redis 캐시 방법 Node.js와 함께
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis 캐시 제공 tooa 안전한 전용된 Redis 캐시, Microsoft에서 관리 액세스 합니다. Microsoft Azure 내의 모든 응용 프로그램에서 캐시에 액세스할 수 있습니다.

이 항목에서는 tooget Azure Redis Cache를 어떻게 시작 Node.js를 사용 하 여 합니다. Azure Redis Cache를 Node.js와 함께 사용하는 방법에 대한 다른 예는 [Azure 웹 사이트에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드](../app-service-web/web-sites-nodejs-chat-app-socketio.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
[node_redis](https://github.com/mranney/node_redis) 설치:

    npm install redis

이 자습서에서는 [node_redis](https://github.com/mranney/node_redis)를 사용합니다. 다른 Node.js 클라이언트를 사용 하 여의 예에 나열 된 hello Node.js 클라이언트에 대 한 hello 개별 설명서를 참조 [Node.js Redis 클라이언트](http://redis.io/clients#nodejs)합니다.

## <a name="create-a-redis-cache-on-azure"></a>Azure에 Redis 캐시 만들기
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hello 호스트 이름 및 액세스 키를 검색 합니다.
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>SSL을 통해 안전 하 게 toohello 캐시를 연결 합니다.
최신 빌드를 hello [node_redis](https://github.com/mranney/node_redis) tooAzure Redis Cache를 연결 하기 위한 지원을 제공 SSL을 사용 합니다. 다음 예제는 hello tooconnect tooAzure Redis Cache를 사용 하 여 6380의 SSL 끝점을 hello 하는 방법을 보여 줍니다. 대체 `<name>` 캐시 hello 이름의 및 `<key>` 사용 하 여 기본 또는 보조 키에 설명 된 대로 hello 이전 [hello 호스트 이름 및 액세스 키를 검색](#retrieve-the-host-name-and-access-keys) 섹션.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> 새 Azure Redis 캐시 인스턴스에 대 한 hello 비 SSL 포트를 사용 하는 사용할 수 없습니다. SSL을 지원 하지 않는 다른 클라이언트를 사용 하는 경우 참조 [어떻게 tooenable hello 비 SSL 포트](cache-configure.md#access-ports)합니다.
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>추가 toohello을 캐시 하 고 검색
다음 예제와 있습니다 tooconnect tooan Azure Redis 캐시 인스턴스를 하 고 저장 하는 방법과 hello 캐시에서 항목을 검색 하는 번호입니다. Redis를 사용 하 여 hello로의 추가 예 [node_redis](https://github.com/mranney/node_redis) 클라이언트 참조 [http://redis.js.org/](http://redis.js.org/)합니다.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

출력:

    OK
    value


## <a name="next-steps"></a>다음 단계
* [캐시 진단을 사용 하도록 설정](cache-how-to-monitor.md#enable-cache-diagnostics) 할 수 있도록 [모니터](cache-how-to-monitor.md) hello 캐시의 상태입니다.
* 읽기 hello 공식 [설명서 Redis](http://redis.io/documentation)합니다.


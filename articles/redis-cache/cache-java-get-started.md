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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Toouse Azure Redis 캐시 방법 Java와 함께
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis Cache 액세스할 수 있도록 tooa 전용된 Redis 캐시를 Microsoft에서 관리 합니다. Microsoft Azure 내의 모든 응용 프로그램에서 캐시에 액세스할 수 있습니다.

이 항목에서는 tooget Azure Redis Cache를 어떻게 시작 Java를 사용 하 여 합니다.

## <a name="prerequisites"></a>필수 조건
[Jedis](https://github.com/xetorthio/jedis) - Redis용 Java 클라이언트

이 자습서에서는 Jedis를 사용하지만 [http://redis.io/clients](http://redis.io/clients)에 나열된 모든 Java 클라이언트를 사용할 수 있습니다.

## <a name="create-a-redis-cache-on-azure"></a>Azure에 Redis 캐시 만들기
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hello 호스트 이름 및 액세스 키를 검색 합니다.
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>SSL을 통해 안전 하 게 toohello 캐시를 연결 합니다.
최신 빌드를 hello [jedis](https://github.com/xetorthio/jedis) tooAzure Redis Cache를 연결 하기 위한 지원을 제공 SSL을 사용 합니다. 다음 예제는 hello tooconnect tooAzure Redis Cache를 사용 하 여 6380의 SSL 끝점을 hello 하는 방법을 보여 줍니다. 대체 `<name>` 캐시 hello 이름의 및 `<key>` 사용 하 여 기본 또는 보조 키에 설명 된 대로 hello 이전 [hello 호스트 이름 및 액세스 키를 검색](#retrieve-the-host-name-and-access-keys) 섹션.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> 새 Azure Redis 캐시 인스턴스에 대 한 hello 비 SSL 포트를 사용 하는 사용할 수 없습니다. SSL을 지원 하지 않는 다른 클라이언트를 사용 하는 경우 참조 [어떻게 tooenable hello 비 SSL 포트](cache-configure.md#access-ports)합니다.
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>추가 toohello을 캐시 하 고 검색
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


## <a name="next-steps"></a>다음 단계
* [캐시 진단을 사용 하도록 설정](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) 할 수 있도록 [모니터](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello 캐시의 상태입니다.
* 읽기 hello 공식 [설명서 Redis](http://redis.io/documentation)합니다.

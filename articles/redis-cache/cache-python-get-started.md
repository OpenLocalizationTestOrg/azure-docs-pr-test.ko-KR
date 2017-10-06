---
title: Azure Redis Cache python aaaHow toouse | Microsoft Docs
description: "Python을 사용하여 Azure Redis Cache를 시작합니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a>Toouse Azure Redis 캐시 방법 python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

이 항목에서는 tooget Azure Redis Cache를 어떻게 시작 Python을 사용 하 여 합니다.

## <a name="prerequisites"></a>필수 조건
[redis-py](https://github.com/andymccurdy/redis-py)를 설치합니다.

## <a name="create-a-redis-cache-on-azure"></a>Azure에 Redis 캐시 만들기
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hello 호스트 이름 및 액세스 키를 검색 합니다.
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>Hello 비 SSL 끝점을 사용 하도록 설정
일부 Redis 클라이언트는 SSL을 지원 하지 않습니다 및 기본 hello [새 Azure Redis 캐시 인스턴스에 대 한 비 SSL 포트를 사용할 수 없습니다.](cache-configure.md#access-ports)합니다. 이 문서 작성 hello 시 hello [redis py](https://github.com/andymccurdy/redis-py) 클라이언트는 SSL을 지원 하지 않습니다. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>추가 toohello을 캐시 하 고 검색
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


`<name>`을 사용 중인 캐시 이름으로 바꾸고 `key`를 사용 중인 액세스 키로 바꿉니다.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png

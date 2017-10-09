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
# <a name="azure-redis-cache-samples"></a>Azure Redis Cache 샘플
이 항목에서는 Azure Redis Cache 샘플, 예: tooa 캐시 연결, 읽기 및는 캐시에서 데이터 tooand 쓰기 hello ASP.NET Redis 캐시 공급자를 사용 하는 시나리오를 다룹니다 목록을 제공 합니다. Hello 샘플의 일부는 다운로드 가능한 프로젝트 있으며 단계별 지침을 제공 일부 코드 조각을 포함 하지만 tooa 다운로드할 수 있는 프로젝트를 연결 하지 않습니다.

## <a name="hello-world-samples"></a>Hello world 샘플
hello이이 섹션의에서 예제에는 Redis 클라이언트를 연결 tooan Azure Redis 캐시 인스턴스를 읽고 쓰는 다양 한 언어를 사용 하 여 데이터 toohello 캐시의 기본 사항 hello를 표시 합니다.

hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 방법을 보여 줍니다 샘플 tooperform 다양 한 캐시 작업 hello를 사용 하 여 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 클라이언트입니다.

이 샘플에서는 다음 작업을 수행하는 방법을 보여줍니다.

* 다양한 연결 옵션 사용
* 동기 및 비동기 작업을 사용 하 여 hello 캐시에서 개체 tooand 읽기 및 쓰기
* 지정 된 키의 Redis MGET/MSET 명령을 tooreturn 값을 사용 하 여
* Redis 트랜잭션 작업 수행
* Redis 목록 및 정렬된 집합 작업
* JsonConvert serializer를 사용하여.NET 개체 저장
* 사용 하 여 Redis 설정 tooimplement 태그 지정
* Redis 클러스터 작업

자세한 내용은 참조 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) github와 더 많은 사용 시나리오에 대 한 설명서 참조 hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) 단위 테스트 합니다.

[Toouse Azure Redis 캐시 방법 python](cache-python-get-started.md) tooget Python 및 hello를 사용 하 여 Azure Redis 캐시를 시작 하는 방법을 보여 줍니다. [redis py](https://github.com/andymccurdy/redis-py) 클라이언트입니다.

[Hello 캐시에서.NET 개체 사용](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) tooand 작성할 수 있습니다. 한 가지 방법은 tooserialize.NET 개체에서는 Azure Redis Cache 인스턴스에서 읽을 합니다. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Redis Cache를 ASP.NET SignalR에 대한 규모 확장 백플레인으로 사용
hello [확장형 백플레인 ASP.NET SignalR 용 Redis Cache 사용](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) 샘플 SignalR 백플레인으로 Azure Redis Cache를 사용 하는 방법을 보여 줍니다. 백플레인에 대한 자세한 내용은 [Redis를 사용한 SignalR 규모 확장](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)을 참조하세요.

## <a name="redis-cache-customer-query-sample"></a>Redis Cache 고객 쿼리 샘플
이 샘플은 캐시의 데이터 액세스와 영구적 저장소의 데이터 액세스 간 성능 비교를 보여 줍니다. 이 샘플에는 두 개의 프로젝트가 있습니다.

* [Redis Cache가 데이터를 캐싱하여 성능을 향상시키는 방법 데모](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [시드는 hello 데모에 대 한 데이터베이스 및 캐시 hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>ASP.NET 세션 상태 및 출력 캐싱
hello [OutputCache 및 SessionState ASP.NET 사용 하 여 Azure Redis Cache toostore](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) 샘플 있습니다 toouse Azure Redis Cache toostore ASP.NET 세션 및 출력 캐시를 사용 하 여 hello에 대 한 공급자 OutputCache 및 SessionState 방법을 보여 줍니다. Redis는 합니다.

## <a name="manage-azure-redis-cache-with-maml"></a>MAML을 사용하여 Azure Redis Cache 관리
hello [관리 Azure Redis Cache Azure 관리 라이브러리를 사용 하 여](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 샘플-Azure 관리 라이브러리 toomanage 방법을 사용할 수 있는 방법을 보여 줍니다 (만들기 / 업데이트 / 삭제) 캐시 합니다. 

## <a name="custom-monitoring-sample"></a>사용자 지정 모니터링 샘플
hello [액세스 Redis 캐시 모니터링 데이터](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 샘플 hello Azure 포털 외부에서 Azure Redis Cache에 대 한 모니터링 데이터를 액세스 하는 방법을 보여 줍니다.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>PHP 및 Redis를 사용하여 작성된 Twitter 스타일 클론
hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) 샘플은 Redis Hello World hello 합니다. Redis 및 hello를 사용 하 여 PHP를 사용 하 여 작성 된 최소한의 Twitter 스타일 소셜 네트워크 복제본 [Predis](https://github.com/nrk/predis) 클라이언트입니다. hello 소스 코드는 매우 간단한 설계 된 toobe 및 hello에서 동일한 시간 tooshow 다른 Redis 데이터 구조입니다.

## <a name="bandwidth-monitor"></a>대역폭 모니터
hello [대역폭 모니터](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) 샘플 hello 클라이언트에서 사용 되는 toomonitor hello 대역폭을 수 있습니다. toomeasure는 대역폭 hello, hello 샘플 hello 캐시 클라이언트 컴퓨터에서 실행, 호출 toohello 캐시를 확인 및 hello 대역폭 모니터 샘플에서 보고 하는 hello 대역폭을 관찰 합니다.


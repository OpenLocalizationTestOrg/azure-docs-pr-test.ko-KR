---
title: "프리미엄 Azure Redis Cache에 대 한 클러스터링 aaaHow tooconfigure Redis | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 Redis 클러스터링은 고급 계층에 대 한 Azure Redis Cache 인스턴스 관리"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Tooconfigure Redis Premium Azure Redis Cache에 대 한 클러스터링 하는 방법
Azure Redis 캐시 캐시 크기 및 기능, 프리미엄 계층 기능 클러스터링, 지 속성 및 가상 네트워크 지원 등을 포함 하 여 hello 선택에서 유연성을 제공 하는 다른 캐시 기능에 있습니다. 이 문서에서는 Azure Redis 캐시 하는 클러스터링에 프리미엄 tooconfigure 방법 설명 인스턴스.

다른 프리미엄 캐시 기능에 대 한 자세한 내용은 참조 [toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)합니다.

## <a name="what-is-redis-cluster"></a>Redis 클러스터란?
Azure Redis Cache는 [Redis에서 구현된 형태의](http://redis.io/topics/cluster-tutorial)Redis 클러스터를 제공합니다. Redis 클러스터와 hello 다음 이점을 얻을 수 있습니다. 

* hello 기능 tooautomatically 여러 노드 중에서 데이터 집합을 분할합니다. 
* 오류 발생 또는 없습니다 toocommunicate hello 나머지 hello 클러스터와는 hello 기능 toocontinue 작업 때 하위 집합 hello 노드. 
* 더 많은 처리량: hello 분할 영역 수를 늘리면 처리량 선형으로 증가 합니다. 
* 더 많은 메모리 크기: hello 분할 영역 수를 늘리면 비례하여 증가 합니다.  

프리미엄 캐시에서의 크기, 처리량 및 대역폭에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.

Azure Redis 클러스터는 각 분할 된 데이터베이스에 있는 복제의 경우 주/복제본 쌍 hello 복제 Azure Redis 캐시 서비스에서 관리 되는 위치는 주/복제본 모델로 제공 됩니다. 

## <a name="clustering"></a>클러스터링
Hello에서 클러스터링을 사용할 수 **새 Redis 캐시** 블레이드 캐시 만들기 중입니다. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Hello에 구성 된 클러스터링 **Redis 클러스터** 블레이드입니다.

![클러스터링][redis-cache-clustering]

Too10 hello 클러스터의 분할 된 데이터베이스를 만들 수 있습니다. 클릭 **Enabled** hello 슬라이더를 이동 하거나 1과 10 사이의 숫자를 입력 하 고 **분할 영역 수** 클릭 **확인**합니다.

각 분할은 Azure에서 관리 되는 주/복제본 캐시 쌍 및 hello 캐시의 총 크기가 hello hello 분할 영역 수 hello 가격 책정 계층에서에서 선택한 hello 캐시 크기를 곱하여 계산 됩니다. 

![클러스터링][redis-cache-clustering-selected]

Hello 캐시는 생성 되 면 tooit 연결 하 고 사용 하 여 방금가 클러스터 되지 않은 캐시와 유사 하 고 Redis hello 캐시 분할 된 데이터베이스 전체의 hello 데이터를 배포 합니다. 진단이 [활성화](cache-how-to-monitor.md#enable-cache-diagnostics), 메트릭 각 분할에 대해 개별적으로 문서화 하 고 수 [볼](cache-how-to-monitor.md) hello Redis 캐시 블레이드에 합니다. 

> [!NOTE]
> 
> 클러스터링을 구성할 때 클라이언트 응용 프로그램에 필요한 몇 가지 사소한 차이점이 있습니다. 자세한 내용은 참조 [필요 합니까 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Hello StackExchange.Redis 클라이언트를 사용한 클러스터링 사용에 대 한 샘플 코드에서 참조 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello 부분의 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>실행 하는에서 hello 클러스터 크기를 변경 합니다. 프리미엄 캐시
실행 중인 프리미엄에 대 한 toochange hello 클러스터 크기 클러스터링 사용된을 클릭 하 여 캐시 **Redis 클러스터 크기** hello에서 **리소스 메뉴**합니다.

> [!NOTE]
> Hello Azure Redis Cache 프리미엄 계층 되었습니다 해제 tooGeneral 가용성 동안 hello Redis 클러스터 크기 기능은 현재 미리 보기에 있습니다.
> 
> 

![Redis 클러스터 크기][redis-cache-redis-cluster-size]

toochange hello 클러스터 크기 hello 슬라이더를 사용 하거나 hello에 1과 10 사이의 숫자를 입력 **분할 영역 수** 텍스트 상자 **확인** toosave 합니다.

> [!NOTE]
> Hello를 실행 하는 클러스터 크기 조정 [마이그레이션](https://redis.io/commands/migrate) 비용이 많이 드는 명령 인 명령의 최소한의 영향에 대 한 것이 좋습니다 사용량이 적은 시간 중에이 작업을 실행 합니다. Hello 마이그레이션 프로세스 중 서버 부하에 스파이크가 나타납니다. 클러스터를 확장 하는 장기 실행 중인 프로세스 및 hello에 걸린 시간에 따라 달라 집니다 hello 키 수와 해당 키와 관련 된 hello 값의 크기입니다.
> 
> 

## <a name="clustering-faq"></a>클러스터링 FAQ
hello 다음 목록에 포함 되어 Azure Redis Cache 클러스터링에 대 한 질문과 대답 toocommonly 있습니다.

* [해야 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [클러스터에서 키를 분산하는 방법](#how-are-keys-distributed-in-a-cluster)
* [만들 수 있습니다. hello 최대 캐시 크기는 무엇입니까?](#what-is-the-largest-cache-size-i-can-create)
* [모든 Redis 클라이언트가 클러스터링을 지원하나요?](#do-all-redis-clients-support-clustering)
* [클러스터링을 사용 하는 toomy 캐시를 연결 하는 방법](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [직접 내 캐시의 분할 된 toohello 개별 데이터베이스를 연결할 수 있습니까?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [이전에 만든된 캐시에 대해 클러스터링을 구성할 수 있나요?](#can-i-configure-clustering-for-a-previously-created-cache)
* [기본 또는 표준 캐시에 클러스터링을 구성할 수 있나요?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [StackExchange.Redis를 사용하고 클러스터링을 수행할 때 MOVE 예외가 발생합니다. 어떻게 해야 하나요?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>해야 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?
* 클러스터링 사용하는 경우 데이터베이스 0만을 사용할 수 있습니다. 클라이언트 응용 프로그램에서 여러 데이터베이스를 사용 하는 경우 0이 아닌 tooa 데이터베이스 tooread 또는 쓰기를 시도 하기 hello 다음 예외가 throw 됩니다. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  자세한 내용은 [Redis 클러스터 사양 - 구현된 하위 집합](http://redis.io/topics/cluster-spec#implemented-subset)을 참조하세요.
* [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/)를 사용하는 경우 1.0.481 이상을 사용해야 합니다. Toohello 캐시 연결 동일 hello를 사용 하 여 [끝점, 포트 및 키](cache-configure.md#properties) 클러스터링을 사용 하지 않은 tooa 캐시를 연결할 때 사용 하는 합니다. hello 유일한 차이점은 모든 읽기 및 쓰기 수행 해야 함을 toodatabase 0입니다.
  
  * 다른 클라이언트는 다른 요구 사항이 있을 수 있습니다. [모든 Redis 클라이언트가 클러스터링을 지원하나요?](#do-all-redis-clients-support-clustering)
* 응용 프로그램에서 단일 명령으로 일괄 처리할 여러 개의 키 작업을 사용 하는 경우 모든 키에 있어야 hello 동일한 분할 합니다. toolocate 키에서 동일한 shard hello 하 참조 [클러스터에서 키는 배포 방법을?](#how-are-keys-distributed-in-a-cluster)
* Redis ASP.NET 세션 상태 제공자를 사용하는 경우 2.0.1 이상을 사용해야 합니다. 참조 [클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>클러스터에서 키를 분산하는 방법
Hello Redis 당 [키 배포 모델](http://redis.io/topics/cluster-spec#keys-distribution-model) 설명서: hello 키 공간 16384 슬롯으로 분할 됩니다. 각 키는 해시 이며 tooone hello 클러스터의 노드를 hello 통해 배포 되는 이러한 슬롯을 할당 합니다. Hello 키의 어느 부분이 여러 키에 있는 해시 된 tooensure 구성할 수는 해시 태그를 사용 하는 동일한 분할 영역 hello 합니다.

* Hello 키의 일부에 포함 되어 있으면 해시 태그-와 키는 `{` 및 `}`, hello 키의 해당 부분에만 키의 해시 슬롯 hello를 결정 하는 hello로 해시 됩니다. Hello에 다음 3 개의 키 hello은 위치 하는 예를 들어 동일한 shard: `{key}1`, `{key}2`, 및 `{key}3` 만 hello 이후 `key` hello 이름의 일부 해시 됩니다. 키 해시 태그 사양의 전체 목록은 [키 해시 태그](http://redis.io/topics/cluster-spec#keys-hash-tags)를 참조하세요.
* 해시는 해시 태그-hello 전체 키 이름 없이 키 사용 됩니다. 따라서 hello hello 캐시의 분할 된 데이터베이스에서 통계적으로 균등 한 분포가 됩니다.

최상의 성능 및 처리량에 대 한 hello 키를 균등 하 게 배포 하는 것이 좋습니다. 키 해시 태그와 함께 사용 하는 경우 hello 응용 프로그램의 책임 tooensure hello 키는 고르게 배포 됩니다.

자세한 내용은 [키 배포 모델](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis 클러스터 데이터 분할](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) 및 [키 해시 태그](http://redis.io/topics/cluster-spec#keys-hash-tags)를 참조하세요.

샘플 코드와 클러스터링 키 hello에서 찾기 작업에 대 한 hello StackExchange.Redis 클라이언트를 사용 하 여 동일한 분할 참조 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello 부분의 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>만들 수 있습니다. hello 최대 캐시 크기는 무엇입니까?
hello 가장 큰 premium 캐시 크기는 53 GB입니다. Too10 분할 530 g B의 최대 크기를 지정 된 데이터베이스를 만들 수 있습니다. 더 큰 크기가 필요한 경우 [추가 요청](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase)이 가능합니다. 자세한 내용은 [Azure Redis Cache 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요.

### <a name="do-all-redis-clients-support-clustering"></a>모든 Redis 클라이언트가 클러스터링을 지원하나요?
Hello에서 모든 클라이언트에서 지원 되는 현재 시간 Redis 클러스터링 사용. 이를 지원하는 클라이언트는 StackExchange.Redis입니다. 다른 클라이언트에 자세한 내용은 참조 hello [hello 클러스터와 재생](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) hello 섹션 [Redis 클러스터 자습서](http://redis.io/topics/cluster-tutorial)합니다.

> [!NOTE]
> StackExchange.Redis 클라이언트를 사용 하는 경우 최신 버전의 hello를 사용 하는 확인 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 올바르게 toowork 클러스터링에 대 한 이상. move 예외에 문제가 있을 경우 자세한 내용은 [move 예외](#move-exceptions) 를 참조하세요.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>클러스터링을 사용 하는 toomy 캐시를 연결 하는 방법
Tooyour 캐시 연결 수 동일 hello를 사용 하 여 [끝점](cache-configure.md#properties), [포트](cache-configure.md#properties), 및 [키](cache-configure.md#access-keys) 클러스터링을 사용 하지 않은 tooa 캐시를 연결할 때 사용 하는 합니다. Redis hello toomanage 없는 hello 백 엔드에 클러스터링 관리 클라이언트에서.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>직접 내 캐시의 분할 된 toohello 개별 데이터베이스를 연결할 수 있습니까?
공식적으로는 지원되지 않습니다. 즉 각각의 분할된 데이터베이스는 캐시 인스턴스로 통칭되는 주/복제본 캐시로 구성됩니다. Hello redis cli 유틸리티를 사용 하 여 hello에 toothese 캐시 인스턴스를 연결할 수 있습니다 [불안정](http://redis.io/download) GitHub에서 hello Redis 리포지토리의 분기입니다. 이 버전 hello로 시작 될 때 기본 지원을 구현 `-c` 전환 합니다. 자세한 내용은 참조 [hello 클러스터와 재생](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) 에 [http://redis.io](http://redis.io) hello에 [Redis 클러스터 자습서](http://redis.io/topics/cluster-tutorial)합니다.

비 ssl에 대 한 명령을 수행 하는 hello를 사용 합니다.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

SSL에서는 `1300N`을 `1500N`으로 대체합니다.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>이전에 만든된 캐시에 대해 클러스터링을 구성할 수 있나요?
현재 캐시를 만들 때만 클러스터링을 사용하도록 설정할 수 있습니다. 클러스터링 tooa 프리미엄 캐시를 추가 하거나 hello 캐시는 생성 후 프리미엄 캐시에서 클러스터링을 제거할 수 있지만 hello 캐시를 만든 후 hello 클러스터 크기를 변경할 수 있습니다. 클러스터링을 사용 및 하나의 분할만 프리미엄 캐시는 hello 없는 클러스터링과 함께 동일한 크기의 프리미엄 캐시와 다릅니다.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>기본 또는 표준 캐시에 클러스터링을 구성할 수 있나요?
클러스터링은 프리미엄 캐시에만 사용할 수 있습니다.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>클러스터링 hello Redis ASP.NET 세션 상태 및 출력 캐싱 공급자와 함께 사용할 수 있습니까?
* **Redis 출력 캐시 공급자** - 변경이 필요하지 않습니다.
* **Redis 세션 상태 공급자** -toouse 클러스터링을 사용 해야 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 높이 거 나 예외를 throw 합니다. 주요 변경 내용입니다. 자세한 내용은 [v2.0.0 주요 변경 세부 사항](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)을 참조하세요.

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>StackExchange.Redis를 사용하고 클러스터링을 수행할 때 MOVE 예외가 발생합니다. 어떻게 해야 하나요?
StackExchange.Redis를 사용하고 있으며 클러스터링을 사용할 때 `MOVE` 예외가 발생하는 경우 [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) 이상을 사용하고 있는지 확인합니다. .NET 응용 프로그램 toouse StackExchange.Redis를 구성 하는 방법에 지침은 [hello 캐시 클라이언트 구성](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)합니다.

## <a name="next-steps"></a>다음 단계
Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.

* [Toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png








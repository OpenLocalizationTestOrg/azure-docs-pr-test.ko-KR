---
title: "프리미엄 Azure Redis Cache에 대 한 aaaHow tooconfigure 데이터 지 속성"
description: "자세한 내용은 방법 tooconfigure 및 프리미엄 계층 Azure Redis 캐시 인스턴스 데이터 유지 관리"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>어떻게 Premium Azure Redis Cache에 대 한 tooconfigure 데이터 지 속성
Azure Redis 캐시 캐시 크기 및 기능, 프리미엄 계층 기능 클러스터링, 지 속성 및 가상 네트워크 지원 등을 포함 하 여 hello 선택에서 유연성을 제공 하는 다른 캐시 기능에 있습니다. 이 문서에서는 Azure Redis 캐시 하는 한 premium에서 tooconfigure 지 속성 방법 설명 인스턴스.

다른 프리미엄 캐시 기능에 대 한 자세한 내용은 참조 [toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)합니다.

## <a name="what-is-data-persistence"></a>데이터 지속성이란?
[지 속성 redis](https://redis.io/topics/persistence) Redis에 저장 된 toopersist 데이터 있습니다. 스냅숏을 하 고 하드웨어 오류가 발생할 경우 로드할 수 있는 hello 데이터를 백업할 수도 있습니다. 이것은 Basic의 이점을 활용 또는 표준 계층 데이터를 hello 모든 메모리에 저장 됩니다 및 다운은 캐시 노드가 되는 경우 오류가 발생 한 경우 데이터가 손실 될 수 있습니다. 

Azure Redis 캐시는 모델을 따르는 hello를 사용 하 여 Redis 지 속성을 제공 합니다.

* **RDB 지 속성** -때 RDB (Redis 데이터베이스)의 지 속성 구성, Azure Redis Cache hello Redis 캐시 구성 가능한 백업 빈도에 따라 이진 형식 toodisk Redis에 대 한 스냅숏을 유지 합니다. 재해 발생 기본 hello와 복제본 캐시 모두 비활성화 하는 hello 캐시 hello 최신 스냅숏을 다시 생성 됩니다. Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages) RDB 지 속성입니다.
* **지 속성 AOF** -때 AOF (Append 유일한 파일)의 지 속성 구성, Azure Redis Cache는 Azure 저장소 계정에는 초 당 최소 한 번 저장 되는 모든 쓰기 작업 tooa 로그를 저장 합니다. 재해 발생 기본 hello와 복제본 캐시 모두 비활성화 하는 hello 캐시 쓰기 작업을 저장 하는 hello를 사용 하 여 다시 생성 됩니다. Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages) AOF 지 속성입니다.

지 속성 hello에서 구성 된 **새 Redis 캐시** 블레이드 hello 및 캐시 만들기 중 **리소스 메뉴** 기존 프리미엄 캐시 합니다.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

프리미엄 가격 책정 계층을 선택한 다음 **Redis 지속성**을 클릭합니다.

![Redis 지속성][redis-cache-persistence]

hello hello 다음 섹션의 단계에 설명 방법을 tooconfigure 새 프리미엄 캐시에 Redis 지 속성입니다. Redis 지 속성 구성 되 면 클릭 **만들기** toocreate Redis 지 속성을 사용 하 여 새 프로그램 프리미엄 캐시 합니다.

## <a name="enable-redis-persistence"></a>Redis 지속성 사용

Redis hello에서 지 속성을 사용 하는 **Redis 데이터 지 속성** 블레이드 중 하나를 선택 하 여 **RDB** 또는 **AOF** 지 속성입니다. 새 캐시의 경우이 블레이드는 hello 이전 섹션에 설명 된 대로 hello 캐시를 만드는 프로세스 동안 액세스 됩니다. 기존 캐시에 대 한 hello **Redis 데이터 지 속성** 블레이드 hello에서 액세스 **리소스 메뉴** 캐시 합니다.

![Redis 설정][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>RDB 지속성 구성

tooenable RDB 지 속성 클릭 **RDB**합니다. 이전에 설정 된 프리미엄 캐시에서 toodisable RDB 지 속성과 클릭 **비활성화**합니다.

![Redis RDB 지속성][redis-cache-rdb-persistence]

tooconfigure hello 백업 간격을 선택는 **백업 빈도** hello 드롭 다운 목록에서 합니다. **15분**, **30분**, **60분**, **6시간**, **12시간** 및 **24시간** 중에서 선택할 수 있습니다. 이 간격은 hello 이전 백업 작업이 성공적으로 완료 되 고이 경과 하면 새 백업을 시작 후 카운트다운을 시작 합니다.

클릭 **저장소 계정** tooselect 저장소 계정 toouse hello 선택한 어느 hello **기본 키** 또는 **보조 키** hello에서 toouse **저장소 키** 드롭 다운 합니다. Hello에 저장소 계정을 선택 해야 hello 캐시와 동일한 지역 및 **프리미엄 저장소** 프리미엄 저장소 처리량이 높은 때문에 계정을 것이 좋습니다. 

> [!IMPORTANT]
> Hello hello에서 원하는 키를 다시 구성 해야 지 속성 계정에 대 한 hello 저장소 키를 다시 생성 하는 경우 **저장소 키** 드롭 다운 합니다.
> 
> 

클릭 **확인** toosave hello 지 속성 구성.

hello 백업 빈도 간격에 경과 되 면 hello (또는 새 캐시에 대 한 첫 번째 백업은 다음 백업)가 시작 됩니다.

## <a name="configure-aof-persistence"></a>AOF 지속성 구성

tooenable AOF 지 속성 클릭 **AOF**합니다. 이전에 설정 된 프리미엄 캐시에서 toodisable AOF 지 속성과 클릭 **비활성화**합니다.

![Redis AOF 지속성][redis-cache-aof-persistence]

tooconfigure AOF 지 속성을 지정 된 **첫 저장소 계정을**합니다. 이 저장소 계정은 hello에 있어야 hello 캐시와 동일한 지역 및 **프리미엄 저장소** 프리미엄 저장소 처리량이 높은 때문에 계정을 것이 좋습니다. 경우에 따라 **두 번째 저장소 계정**이라는 추가 저장소 계정을 구성할 수 있습니다. 두 번째 저장소 계정이 구성 된 경우 hello 쓰기 toohello 복제본 캐시가 쓰여집니다 toothis 두 번째 저장소 계정. 각 구성 된 저장소 계정에 대해 선택 하거나 hello **기본 키** 또는 **보조 키** hello에서 toouse **저장소 키** 드롭 다운 합니다. 

> [!IMPORTANT]
> Hello hello에서 원하는 키를 다시 구성 해야 지 속성 계정에 대 한 hello 저장소 키를 다시 생성 하는 경우 **저장소 키** 드롭 다운 합니다.
> 
> 

AOF 지 속성을 사용 하는 경우 작업 toohello 캐시 toohello 저장소 계정 또는 계정을 두 번째 저장소 계정을 구성 하는 경우 지정 된 저장 작성 합니다. 치명적인 오류의 hello 이벤트에서 모두 다운은 hello 기본 및 복제본 캐시 hello 저장된 AOF 로그는 toorebuild hello 캐시를 사용 합니다.

## <a name="persistence-faq"></a>지속성 FAQ
hello 다음 목록에 포함 되어 Azure Redis Cache 지 속성에 대 한 질문과 대답 toocommonly 있습니다.

* [이전에 만든 캐시에서 지속성을 사용할 수 있나요?](#can-i-enable-persistence-on-a-previously-created-cache)
* [사용할 수 있습니까 hello에서 AOF 및 RDB 지 속성 동시?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [어떤 지속성 모델을 선택해야 하나요?](#which-persistence-model-should-i-choose)
* [Tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하는 경우 어떻게 됩니까?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>RDB 지속성
* [Hello 캐시를 만든 후 hello RDB 백업 빈도 변경 합니까?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [새 백업을 만들어질 때 toohello 오래 RDB 백업 되나요?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>AOF 지속성
* [두 번째 저장소 계정은 언제 사용해야 하나요?](#when-should-i-use-a-second-storage-account)
* [AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Hello 두 번째 저장소 계정을 제거 하는 방법](#how-can-i-remove-the-second-storage-account)
* [다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>이전에 만든 캐시에서 지속성을 사용할 수 있나요?
예, Redis 지속성은 캐시를 만들 때와 기존 프리미엄 캐시에서 모두 구성할 수 있습니다.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>사용할 수 있습니까 hello에서 AOF 및 RDB 지 속성 동시?

아니요,만 RDB 또는 AOF, 하나만 hello에를 사용할 수 있습니다 동시 합니다.

### <a name="which-persistence-model-should-i-choose"></a>어떤 지속성 모델을 선택해야 하나요?

처리량에 대 한 몇 가지 영향이 있는 모든 쓰기 tooa 로그를 저장 하는 AOF 지 속성, RDB와 비교 hello에 따라 백업을 저장 하는 지 속성 구성 백업 간격 성능에 미치는 영향을 최소화 합니다. 주요 목표는 toominimize 데이터 손실, 프로그램과 캐시에 대 한 처리량이 감소를 처리할 수 있는 경우에 AOF 지 속성을 선택 합니다. 캐시에 toomaintain 최적 처리량을 원하는 하지만 계속 데이터 복구 하기 위한 메커니즘을 실행할 경우 RDB 지 속성을 선택 합니다.

* Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#rdb-advantages) 및 [단점](https://redis.io/topics/persistence#rdb-disadvantages) RDB 지 속성입니다.
* Hello에 대 한 자세한 [장점](https://redis.io/topics/persistence#aof-advantages) 및 [단점](https://redis.io/topics/persistence#aof-disadvantages) AOF 지 속성입니다.

AOF 지속성을 사용하는 경우 성능에 대한 자세한 내용은 [AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)를 참조하세요.

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하는 경우 어떻게 됩니까?

RDB 및 AOF 지속성:

* Tooa 더 큰 크기를 조정 했을 경우 아무 영향도 끼치지 않습니다.
* Tooa 더 작은 크기를 조정 했 고 사용자 지정 [데이터베이스](cache-configure.md#databases) hello 보다 크면 설정 [데이터베이스 제한](cache-configure.md#databases) 복원 되지 않으면 해당 데이터베이스의 데이터에 새 크기에 대 한 합니다. 자세한 내용은 [사용자 지정 데이터베이스 설정이 크기 조정 동안 영향을 받나요?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Tooa 더 작은 크기를 조정 했 hello 더 작은 크기 toohold 모든 hello 데이터 hello 마지막 백업, 키를 제거 하는 hello 복원 프로세스 중에 충분 한 공간이 없는 경우 일반적으로 사용 하 여 hello [allkeys lru](http://redis.io/topics/lru-cache) 제거 정책입니다.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Hello 캐시를 만든 후 hello RDB 백업 빈도 변경 합니까?
예, hello hello에 RDB 지 속성에 대 한 백업 빈도 변경할 수 있습니다 **Redis 데이터 지 속성** 블레이드입니다. 자세한 내용은 [Redis 지속성 구성](#configure-redis-persistence)을 참조하세요.

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>RDB 백업 주기가 60분인데 왜 백업 사이 간격이 60분 이상이 되나요?
hello RDB 지 속성 백업 빈도 간격 hello 이전 백업 프로세스가 성공적으로 완료 될 때까지 시작 되지 않습니다. Hello 백업 빈도 제한은 60 분 하는 경우 전체 백업 프로세스가 15 분 toosuccessfully 걸리는 hello 다음 백업 hello 후 75 분의 시작 시간 hello 이전 백업 될 때까지 시작 되지 않습니다.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>새 백업을 만들어질 때 toohello 오래 RDB 백업 되나요?
가장 최근의 hello 제외한 모든 RDB 지 속성 백업은 자동으로 삭제 됩니다. 즉시 삭제되지 않을 수 있으나 오래된 백업을 무한정 유지하지는 않습니다.


### <a name="when-should-i-use-a-second-storage-account"></a>두 번째 저장소 계정은 언제 사용해야 하나요?

Hello 캐시에 대 한 예상된 설정 작업 보다 더 높은 있다고 판단 되 면 AOF 지 속성에 대 한 두 번째 저장소 계정을 사용 해야 합니다.  Hello 보조 저장소 계정 설정을 사용 하는 캐시 저장소 대역폭 제한에 도달 하지 않습니다.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>AOF 지속성이 내 캐시의 처리량, 대기 시간 또는 성능에 영향을 미치나요?

AOF 지 속성에 영향을 줍니다 처리량으로 약 15%-20% 최대 부하 미달 hello 캐시 하는 경우 (CPU 및 서버 부하 둘 다의 90%). Hello 캐시 이러한 한도 내에 있을 때 대기 시간 문제 되지 있어야 합니다. 그러나 hello 캐시 됩니다 이러한 한도 더 빨리에 도달할 AOF 사용 하도록 설정 합니다.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Hello 두 번째 저장소 계정을 제거 하는 방법

Hello toobe hello 동일 hello 첫 번째 저장소 계정으로는 두 번째 저장소 계정을 설정 하 여 hello AOF 지 속성 보조 저장소 계정을 제거할 수 있습니다. 자세한 내용은 [AOF 지속성 구성](#configure-aof-persistence)을 참조하세요.

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>다시 쓰기란 무엇이며 내 캐시에 어떤 영향을 미치나요?

Hello AOF 파일 충분 해지면에서 다시 작성 hello 캐시에서 자동으로 대기 됩니다. hello 재작성 크기가 조정 되어 hello AOF 파일 hello 최소한 필요한 작업 toocreate hello 현재 데이터 집합의 집합으로입니다. 를 캡슐화 하는 동안 큰 데이터 집합으로 처리할 때 tooreach 성능 한도 더 빨리 예상 합니다. 다시 작성이 이벤트가 발생 작은 종종 hello AOF 파일, 더 큰 수 없지만 때 자주 발생 하는 시간이 많이 걸립니다.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>AOF가 설정된 캐시의 크기를 조정하는 경우 어떻게 되나요?

크기 조정의 hello 시 hello AOF 파일 훨씬 큰 경우에 다음 hello 크기 조정 작업 tootake 것은 수 파일을 다시 로드 hello 크기 조정을 마친 후 이후 예상 보다 오래 것 기대 합니다.

확장에 대 한 자세한 내용은 참조 하십시오. [tooa 다른 크기 조정 했을 I 및 크기 조정 작업이 hello 이전 작성 된 백업을 복원 하면 어떻게 되나요?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>저장소에서 AOF 데이터는 어떤 방식으로 구성되나요?

AOF 파일에 저장 된 데이터는 hello 데이터 toostorage 저장 노드 tooincrease 성능 당 여러 페이지 blob으로 구분 됩니다. hello 다음 표에 표시 페이지 blob 수는 각 가격 책정 계층에 사용 됩니다.

| 프리미엄 계층 | Blob |
|--------------|-------|
| P1           | 분할당 4    |
| P2           | 분할당 8    |
| P3           | 분할당 16   |
| P4           | 분할당 20   |

클러스터링을 사용 하면 hello 캐시에 있는 각 분할에 hello 이전 표에 표시 된 페이지 blob 자체 집합이 있습니다. 예를 들어 분할이 3개 있는 P2 캐시는 24개 페이지 Blob에 해당 AOF 파일을 분산합니다(분할당 8 Blob, 3개 분할).

다시 쓰기 후 2개의 AOF 파일 집합이 저장소에 존재합니다. Hello 백그라운드에서 발생 하 고 hello 다시 쓰는 동안 toohello 캐시 전송 되는 집합 작업이 toohello 두 번째 세트를 추가 하는 동안 toohello 파일의 첫 번째 집합을 추가 하는 다시 작성 하세요. 오류가 발생한 경우 백업은 다시 쓰기 동안 일시적으로 저장되지만 다시 쓰기가 끝난 후에 즉시 삭제됩니다.


## <a name="next-steps"></a>다음 단계
Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.

* [Toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png

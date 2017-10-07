---
title: Azure Redis Cache aaaHow tooconfigure | Microsoft Docs
description: "Azure Redis Cache에 대 한 hello 기본 Redis 구성 이해 하 고 자세한 방법을 tooconfigure Azure Redis 캐시 인스턴스"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Azure Redis 캐시 하는 tooconfigure 방법
이 항목에서는 tooreview 및 업데이트 하면 Azure Redis 캐시 인스턴스에 대 한 구성 및 Azure Redis 캐시 인스턴스에 대 한 표지 hello 기본 Redis 서버 구성 hello 하는 방법을 설명 합니다.

> [!NOTE]
> 구성 및 프리미엄 캐시 기능 사용에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconfigure 지 속성](cache-how-to-premium-persistence.md), [어떻게 클러스터링 tooconfigure](cache-how-to-premium-clustering.md), 및 [tooconfigure 가상 네트워크를 지 원하는 방법 ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Redis 캐시 설정 구성
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Azure Redis 캐시 설정은 보고 되며 hello에 구성 된 **Redis Cache** hello를 사용 하 여 블레이드 **리소스 메뉴**합니다.

![Redis 캐시 설정](./media/cache-configure/redis-cache-settings.png)

보고 구성 하는 hello hello를 사용 하 여 설정을 다음 **리소스 메뉴**합니다.

* [개요](#overview)
* [활동 로그](#activity-log)
* [액세스 제어(IAM)](#access-control-iam)
* [태그](#tags)
* [문제 진단 및 해결](#diagnose-and-solve-problems)
* [설정](#settings)
    * [액세스 키](#access-keys)
    * [고급 설정](#advanced-settings)
    * [Redis 캐시 관리자](#redis-cache-advisor)
    * [규모](#scale)
    * [Redis 클러스터 크기](#cluster-size)
    * [Redis 데이터 지속성](#redis-data-persistence)
    * [업데이트 예약](#schedule-updates)
    * [지역에서 복제](#geo-replication)
    * [Virtual Network](#virtual-network)
    * [방화벽](#firewall)
    * [속성](#properties)
    * [잠금](#locks)
    * [자동화 스크립트](#automation-script)
* [관리](#administration)
    * [데이터 가져오기](#importexport)
    * [데이터 내보내기](#importexport)
    * [Reboot](#reboot)
* [모니터링](#monitoring)
    * [Redis 메트릭](#redis-metrics)
    * [경고 규칙](#alert-rules)
    * [진단](#diagnostics)
* [설정 지원 및 문제 해결](#support-amp-troubleshooting-settings)
    * [리소스 상태](#resource-health)
    * [새 지원 요청](#new-support-request)


## <a name="overview"></a>개요

**개요**에서는 이름, 포트, 가격 책정 계층 및 선택한 캐시 메트릭과 같은 캐시에 대한 기본 정보를 제공합니다.

### <a name="activity-log"></a>활동 로그

클릭 **활동 로그** tooview 작업 캐시에서 수행 합니다. 사용할 수도 있습니다 tooexpand 필터링이 뷰 tooinclude 기타 참고 자료. 감사 로그 작업에 대한 자세한 내용은 [Resource Manager를 사용하는 감사 작업](../azure-resource-manager/resource-group-audit.md)을 참조하세요. Azure Redis Cache 이벤트 모니터링에 대한 자세한 내용은 [작업 및 경고](cache-how-to-monitor.md#operations-and-alerts)를 참조하세요.

### <a name="access-control-iam"></a>액세스 제어(IAM)

hello **액세스 제어 (IAM)** 섹션 지원을 제공 역할 기반 액세스 제어 (RBAC)에 대 한 hello Azure 포털 toohelp 조직 충족에 대 한 액세스 관리 요구 사항을 단순히 정확 하 게 합니다. 자세한 내용은 참조 [hello Azure 포털의에서 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.

### <a name="tags"></a>태그들

hello **태그** 섹션 리소스 구성할 수 있도록 도와줍니다. 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.


### <a name="diagnose-and-solve-problems"></a>문제 진단 및 해결

클릭 **진단 및 문제 해결** toobe 전략 및 일반적인 문제 해결을 위한 제공 합니다.



## <a name="settings"></a>설정
hello **설정을** 섹션 tooaccess 있으며 hello 다음 캐시에 대 한 설정을 구성 합니다.

* [액세스 키](#access-keys)
* [고급 설정](#advanced-settings)
* [Redis 캐시 관리자](#redis-cache-advisor)
* [규모](#scale)
* [Redis 클러스터 크기](#cluster-size)
* [Redis 데이터 지속성](#redis-data-persistence)
* [업데이트 예약](#schedule-updates)
* [지역에서 복제](#geo-replication)
* [Virtual Network](#virtual-network)
* [방화벽](#firewall)
* [속성](#properties)
* [잠금](#locks)
* [자동화 스크립트](#automation-script)



### <a name="access-keys"></a>액세스 키
클릭 **선택키가** tooview 또는 regenerate hello 액세스 캐시에 대 한 키입니다. 이러한 키는 tooyour 캐시를 연결 하는 hello 클라이언트에서 사용 됩니다.

![Redis 캐시 액세스 키](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>고급 설정
hello 다음 설정에 구성 된 hello **고급 설정** 블레이드입니다.

* [액세스 포트](#access-ports)
* [메모리 정책](#memory-policies)
* [Keyspace 알림(고급 설정)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>액세스 포트
비 SSL 액세스는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다. tooenable hello 비 SSL 포트를 클릭 하 여 **아니요** 에 대 한 **SSL 통해서만 액세스 허용** hello에 **고급 설정** 블레이드에 대 한 클릭 한 다음 **저장**합니다.

![Redis 캐시 액세스 포트](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>메모리 정책
hello **최대 메모리 정책**, **maxmemory 예약**, 및 **maxfragmentationmemory 예약** hello 설정을 **고급 설정**블레이드 hello 캐시에 대 한 hello 메모리 정책을 구성 합니다.

![Redis 캐시 Maxmemory 정책](./media/cache-configure/redis-cache-maxmemory-policy.png)

**최대 메모리 정책** hello 캐시의 제거 정책 hello를 구성 하 고 다음 제거 정책을 hello에서 toochoose 있습니다.

* `volatile-lru`-hello 기본값입니다.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

`maxmemory` 정책에 대한 자세한 내용은 [제거 정책](http://redis.io/topics/lru-cache#eviction-policies)을 참조하세요.

hello **maxmemory 예약** 장애 조치 중 복제와 같은 캐시가 비 작업에 대해 예약 된 mb에서 hello 메모리 양을 구성 합니다. 이 값으로 설정 하면 보다 일관 된 Redis 서버 환경을 toohave 부하 변경 될 때. 이 값은 쓰기 작업이 많은 워크로드에서 더 높게 설정되어야 합니다. 이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.

hello **maxfragmentationmemory 예약** 메모리 조각화에 대 한 예약 된 tooaccommodate은 mb에서 hello 메모리 양을 구성 합니다. 이 값으로 설정 하면 toohave 보다 일관 된 Redis 서버 환경을 hello 캐시가 가득 차거나 닫기 toofull 및 hello 조각화 비율이 높습니다도 하는 경우. 이러한 작업을 위해 메모리가 예약된 경우 캐시된 데이터의 저장에는 사용할 수 없습니다.

새 메모리 예약 값을 선택할 때 한 가지 tooconsider (**maxmemory 예약** 또는 **maxfragmentationmemory 예약**)는 이러한 변경으로 이미 실행 중인 캐시에 미칠 수 있는 많은 양의 데이터가 합니다. 예를 들어, 49 g b의 데이터를 53GB 캐시가 hello 예약 값 too8 GB 변경 한 후이 too45 GB 다운 hello 시스템에 대 한 최대 사용 가능한 메모리를 hello 삭제 합니다. 경우 현재 `used_memory` 또는 사용자의 `used_memory_rss` 45 GB의 hello 새 제한 보다 더 높은 값은 다음 hello 시스템 있는 tooevict 데이터 둘 다를 때까지 됩니다 `used_memory` 및 `used_memory_rss` 45 GB 미만입니다. 제거는 서버 부하 및 메모리 조각화를 증가시킬 수 있습니다. `used_memory` 및 `used_memory_rss`와 같은 캐시 메트릭에 대한 자세한 내용은 [사용 가능한 메트릭 및 보고 간격](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)을 참조하세요.

> [!IMPORTANT]
> hello **maxmemory 예약** 및 **maxfragmentationmemory 예약** 설정이 있습니다만 표준 및 프리미엄 캐시 합니다.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Keyspace 알림(고급 설정)
Hello에 알림이 구성 되어 있어 실제로 redis **고급 설정** 블레이드입니다. 키 스페이스 알림에서 특정 이벤트가 발생할 때 클라이언트 tooreceive 알림의 허용 합니다.

![Redis 캐시 고급 설정](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> 키 스페이스 알림 및 hello **키 스페이스 알림-이벤트** 설정을 표준 및 프리미엄 캐시에 사용할 수 있는 합니다.
> 
> 

자세한 내용은 [Redis Keyspace 알림](http://redis.io/topics/notifications)을 참조하세요. 샘플 코드에 대 한 참조 hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) hello에 대 한 파일 [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 샘플.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis 캐시 관리자
hello **Redis 캐시 관리자** 블레이드에서 캐시에 대 한 권장 사항을 표시 합니다. 정상적으로 작동하는 중에는 추천이 표시되지 않습니다. 

![권장 사항](./media/cache-configure/redis-cache-no-recommendations.png)

Hello에 경고가 표시 된 높은 메모리 사용량, 네트워크 대역폭, 서버 부하 등 캐시 hello 작업 중에 모든 조건의 상황이 발생 하면 **Redis Cache** 블레이드입니다.

![권장 사항](./media/cache-configure/redis-cache-recommendations-alert.png)

Hello에서 추가 정보를 확인할 수 있습니다 **권장 사항을** 블레이드입니다.

![권장 사항](./media/cache-configure/redis-cache-recommendations.png)

Hello에 이러한 메트릭을 모니터링할 수 있습니다 [모니터링 차트](cache-how-to-monitor.md#monitoring-charts) 및 [사용 현황 차트](cache-how-to-monitor.md#usage-charts) hello의 섹션 **Redis Cache** 블레이드입니다.

가격 책정 계층마다 클라이언트 연결, 메모리 및 대역폭에 대한 제한이 다릅니다. 캐시가 오랫동안 이러한 메트릭의 최대 용량에 근접하면 추천이 생성됩니다. Hello 메트릭 및 제한 사항을 검토 하 여 hello에 대 한 자세한 내용은 **권장 사항을** 도구 hello 다음 표를 참조 하십시오.

| Redis Cache 메트릭 | 자세한 정보 |
| --- | --- |
| 네트워크 대역폭 사용량 |[캐시 성능 - 사용 가능한 대역폭](cache-faq.md#cache-performance) |
| 연결된 클라이언트 |[기본 Redis 서버 구성 - maxclients](#maxclients) |
| 서버 부하 |[사용 현황 차트 - Redis 서버 부하](cache-how-to-monitor.md#usage-charts) |
| 메모리 사용량 |[캐시 성능 - 크기](cache-faq.md#cache-performance) |

tooupgrade 캐시를 클릭 하 여 **지금 업그레이드** toochange hello 가격 책정 계층 및 [배율](#scale) 캐시 합니다. 가격 책정 계층 선택에 대한 자세한 내용은 [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)를 참조하세요.


### <a name="scale"></a>확장
클릭 **배율** tooview 또는 변경 hello 가격 책정 계층에 대 한 캐시 합니다. 확장에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooScale Azure Redis 캐시](cache-how-to-scale.md)합니다.

![Redis Cache 가격 책정 계층](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Redis 클러스터 크기
클릭 **(미리 보기) Redis 클러스터 크기** toochange hello 클러스터 크기를 실행 중인 premium에 대 한 캐시 클러스터링을 사용 합니다.

> [!NOTE]
> Azure Redis Cache 프리미엄 계층 되었습니다 hello 하는 동안 tooGeneral 가용성, hello Redis 클러스터 크기 기능을 해제 하는 현재 미리 보기 중입니다.
> 
> 

![Redis 클러스터 크기](./media/cache-configure/redis-cache-redis-cluster-size.png)

toochange hello 클러스터 크기 hello 슬라이더를 사용 하거나 hello에 1과 10 사이의 숫자를 입력 **분할 영역 수** 텍스트 상자 **확인** toosave 합니다.

> [!IMPORTANT]
> Redis 클러스터링은 프리미엄 캐시에만 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](cache-how-to-premium-clustering.md)합니다.
> 
> 


### <a name="redis-data-persistence"></a>Redis 데이터 지속성
클릭 **Redis 데이터 지 속성** tooenable, 해제 또는 프리미엄 캐시에 대 한 데이터 지 속성을 구성 합니다. Azure Redis Cache는 [RDB 지속성](cache-how-to-premium-persistence.md#configure-rdb-persistence) 또는 [AOF 지속성](cache-how-to-premium-persistence.md#configure-aof-persistence)을 사용하여 Redis 지속성을 제공합니다.

자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 지 속성 tooconfigure](cache-how-to-premium-persistence.md)합니다.


> [!IMPORTANT]
> Redis 데이터 지속성은 프리미엄 캐시에만 사용할 수 있습니다. 
> 
> 

### <a name="schedule-updates"></a>업데이트를 예약
hello **업데이트를 예약할** 블레이드 toodesignate 캐시에 대 한 Redis 서버 업데이트에 대 한 유지 관리 기간을 수 있습니다. 

> [!IMPORTANT]
> tooRedis 서버 업데이트 및 Azure 업데이트 또는 hello 캐시를 호스트 하는 hello Vm의 toohello 운영 체제를 업데이트 하지 tooany hello 유지 관리 기간에 적용 됩니다.
> 
> 

![업데이트를 예약](./media/cache-configure/redis-schedule-updates.png)

toospecify 유지 관리 기간 hello 원하는 일 수를 확인 합니다. 각 날에 대 한 hello 유지 관리 창 시작 시간을 지정 고를 클릭 **확인**합니다. Hello 유지 관리 기간에 UTC를 참고 합니다. 

> [!IMPORTANT]
> hello **업데이트를 예약할** 기능은 프리미엄 계층 캐시에 사용할 수만 있습니다. 자세한 내용 및 지침은 [Azure Redis Cache 관리 - 업데이트 예약](cache-administration.md#schedule-updates)을 참조하세요.
> 
> 

### <a name="geo-replication"></a>지역에서 복제

hello **지리적 복제** 블레이드 두 프리미엄 계층 Azure Redis Cache 인스턴스 연결을 위한 메커니즘을 제공 합니다. 캐시가 하나는 기본 연결 된 캐시 hello 및 hello hello 보조 연결 캐시로 다른으로 지정 됩니다. hello 보조 연결 된 캐시는 읽기 전용 및 서 면된 toohello 기본 캐시는 데이터 toohello 보조 연결 된 캐시를 복제 합니다. 이 기능은 Azure 지역에서 사용 되는 tooreplicate 캐시 수 있습니다.

> [!IMPORTANT]
> **지역에서 복제**는 프리미엄 계층 캐시에서만 사용할 수 있습니다. 자세한 내용 및 지침에 대 한 참조 [어떻게 Azure Redis Cache에 대 한 지리적 복제 tooconfigure](cache-how-to-geo-replication.md)합니다.
> 
> 

### <a name="virtual-network"></a>가상 네트워크
hello **가상 네트워크** 섹션 캐시에 대 한 tooconfigure hello 가상 네트워크 설정을 수 있습니다. VNET을 사용 하 여 프리미엄 캐시를 만들기에 대 한 내용은 지원 하 고 해당 설정을 업데이트 하는, 참조 [tooconfigure 가상 네트워크는 프리미엄 Azure Redis Cache에 대 한 지원 방법](cache-how-to-premium-vnet.md)합니다.

> [!IMPORTANT]
> 가상 네트워크 설정은 캐시를 만드는 동안 VNET 지원을 통해 구성된 프리미엄 캐시에만 제공됩니다. 
> 
> 

### <a name="firewall"></a>방화벽

클릭 **방화벽** tooview 고 프리미엄 Azure Redis Cache에 대 한 방화벽 규칙을 구성 합니다.

![방화벽](./media/cache-configure/redis-firewall-rules.png)

시작 및 끝 IP 주소 범위를 사용하여 방화벽 규칙을 지정할 수 있습니다. 방화벽 규칙을 구성 하는 경우 hello 클라이언트 연결만 지정 IP 주소 범위 toohello 캐시에 연결할 수 있습니다. 방화벽 규칙을 저장할 때 연기 되는 짧은 hello 적용 되므로 전에 합니다. 이러한 지연 시간은 일반적으로 1분 미만입니다.

> [!IMPORTANT]
> 방화벽 규칙이 구성된 경우에도 Azure Redis Cache 모니터링 시스템에서의 연결은 항상 허용됩니다.
> 
> 방화벽 규칙은 프리미엄 계층 캐시에만 사용할 수 있습니다.
> 
> 

### <a name="properties"></a>properties
클릭 **속성** hello 캐시 끝점 및 포트 등 캐시에 대 한 tooview 정보입니다.

![Redis 캐시 속성](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>잠금
hello **잠급니다** toolock 구독, 리소스 그룹 또는 리소스 tooprevent 섹션에서는 있습니다 다른 조직의 사용자에 실수로 삭제 하거나 중요 한 리소스를 수정 합니다. 자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.

### <a name="automation-script"></a>자동화 스크립트

클릭 **자동화 스크립트** toobuild 향후 배포에 배포 된 리소스의 템플릿 내보내기 및 합니다. 템플릿 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 참조하세요.

## <a name="administration-settings"></a>관리 설정
hello 설정을 hello **관리** 섹션 허용 tooperform hello 캐시에 대 한 관리 작업을 수행 합니다. 

![관리](./media/cache-configure/redis-cache-administration.png)

* [데이터 가져오기](#importexport)
* [데이터 내보내기](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>가져오기/내보내기
가져오기/내보내기는 내보내고 Azure 저장소 계정에서 프리미엄 캐시 tooa 페이지 blob에서 Redis 캐시 데이터베이스 (RDB) 스냅숏 내보내기 hello 캐시에 tooimport 및 내보내기 데이터 허용 하는 Azure Redis Cache 데이터 관리 작업. 가져오기/내보내기 toomigrate 서로 다른 Azure Redis Cache 인스턴스 간에 사용 하면 또는 hello 캐시 사용 하기 전에 데이터를 채웁니다.

가져오기에는 클라우드 또는 Linux, Windows 또는 Amazon 웹 서비스 등과 같은 모든 클라우드 공급자에서 실행 되는 Redis를 포함 하 여 환경에서 실행 중인 모든 Redis 서버에서 사용 되는 toobring Redis 호환 RDB 파일 일 수 있습니다. 데이터 가져오기는 쉽게 toocreate 미리 채워진된 데이터와 함께 캐시 됩니다. Hello 가져오기 프로세스 동안 Azure Redis Cache hello RDB 파일을 Azure 저장소에서 메모리에 로드 한 다음 hello 캐시로 hello 키를 삽입 합니다.

내보내기는 Azure Redis Cache tooRedis 호환 RDB 파일에 저장 된 tooexport hello 데이터 수 있습니다. Azure Redis Cache 인스턴스 tooanother 또는 tooanother Redis 서버 하나에서이 기능 toomove 데이터를 사용할 수 있습니다. Hello 내보내기 과정에서 임시 파일 VM 호스트 hello Azure Redis Cache 서버 인스턴스 및 hello 파일은 저장소 계정을 지정 하는 업로드 된 toohello hello에 만들어집니다. 실패 또는 성공 상태가 hello 내보내기 작업이 완료 되 면 hello 임시 파일이 삭제 됩니다.

> [!IMPORTANT]
> 가져오기/내보내기는 프리미엄 계층 캐시에만 제공됩니다. 자세한 내용 및 지침은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.
> 
> 

### <a name="reboot"></a>Reboot
hello **재부팅** 블레이드 캐시 tooreboot hello 노드를 허용 합니다. 이 다시 부팅 기능을 사용 하면 있습니다 tootest 복구를 위한 응용 프로그램 캐시 노드 오류가 없는 경우.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

프리미엄 캐시 클러스터링을 사용 해야 하는 경우에 hello 캐시 tooreboot의 어떤 분할 영역을 선택할 수 있습니다.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot 하나 이상의 노드 캐시의 hello 원하는 노드를 선택 하 고 클릭 **재부팅**합니다. 프리미엄 캐시 클러스터링을 사용 해야 하는 경우 hello 분할 tooreboot 선택한 다음 클릭 **재부팅**합니다. 몇 분 후 hello 선택한 노드 다시 부팅 하 고 몇 분 후 다시 온라인 상태로 전환 됩니다.

> [!IMPORTANT]
> 이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다. 자세한 내용 및 지침은 [Azure Redis Cache 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.
> 
> 


## <a name="monitoring"></a>모니터링

hello **모니터링** tooconfigure 진단 및 Redis 캐시에 대 한 모니터링 섹션에서는 있습니다. Azure Redis 캐시 모니터링 및 진단에 대 한 자세한 내용은 참조 하십시오. [어떻게 toomonitor Azure Redis 캐시](cache-how-to-monitor.md)합니다.

![진단](./media/cache-configure/redis-cache-diagnostics.png)

* [Redis 메트릭](#redis-metrics)
* [경고 규칙](#alert-rules)
* [진단](#diagnostics)

### <a name="redis-metrics"></a>Redis 메트릭
클릭 **메트릭 Redis** 너무[메트릭을 볼](cache-how-to-monitor.md#view-cache-metrics) 캐시 합니다.

### <a name="alert-rules"></a>경고 규칙

클릭 **규칙 경고** tooconfigure 경고 Redis 캐시 메트릭을 기반으로 합니다. 자세한 내용은 [경고](cache-how-to-monitor.md#alerts)를 참조하세요.

### <a name="diagnostics"></a>진단

기본적으로 Azure Monitor의 캐시 메트릭은 [30일 동안 저장](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)되었다가 삭제됩니다. toopersist 30 일 이상에 대 한 사용자 캐시 메트릭을 클릭 **진단** 너무[hello 저장소 계정 구성](cache-how-to-monitor.md#export-cache-metrics) toostore 캐시 진단을 사용 합니다.

>[!NOTE]
>추가 tooarchiving 프로그램 캐시 메트릭을 toostorage 수도 있습니다 [스트리밍할 tooan 이벤트 허브 또는 tooLog 분석 보내기](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)합니다.
>
>

## <a name="support--troubleshooting-settings"></a>설정 지원 및 문제 해결
hello 설정을 hello **지원 + 문제 해결** 섹션 캐시 관련 문제 해결에 대 한 옵션을 제공 합니다.

![설정 지원 + 문제 해결](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [리소스 상태](#resource-health)
* [새 지원 요청](#new-support-request)

### <a name="resource-health"></a>리소스 상태
**리소스 상태** 기능은 리소스를 감시하고 예상대로 실행되는지를 알려줍니다. Hello Azure 리소스 상태 관리 서비스에 대 한 자세한 내용은 참조 [Azure 리소스 상태 개요](../resource-health/resource-health-overview.md)합니다.

> [!NOTE]
> 리소스 상태를 현재 없습니다 tooreport 가상 네트워크에서 호스트 되는 Azure Redis 캐시 인스턴스의 hello 상태에 있습니다. 자세한 내용은 [VNET에서 캐시를 호스팅하는 경우 모든 캐시 기능이 작동하나요?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>새 지원 요청
클릭 **새로운 지원 요청** tooopen 캐시에 대 한 지원 요청.





## <a name="default-redis-server-configuration"></a>기본 Redis 서버 구성
새 Azure Redis Cache 인스턴스는 다음 기본 Redis 구성 값에는 hello로 구성 됩니다.

> [!NOTE]
> 이 섹션의 hello 설정을 hello를 사용 하 여 변경할 수 없습니다 `StackExchange.Redis.IServer.ConfigSet` 메서드. 이 메서드는이 섹션의 hello 명령 중 하나를 예외와 유사한 toohello 다음 throw 됩니다.  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> 와 같은 구성할 수 있는 모든 값 **최대 메모리 정책**, hello Azure 포털 또는 Azure CLI 또는 PowerShell과 같은 명령줄 관리 도구를 통해 구성할 수 있습니다.
> 
> 

| 설정 | 기본값 | 설명 |
| --- | --- | --- |
| `databases` |16 |데이터베이스의 hello 기본 수는 16 하지만 가격 책정 계층 다른 숫자에 따라 hello를 구성할 수 있습니다. <sup>1</sup> hello 기본 데이터베이스는 DB 0을 사용 하 여 각 연결 별로 다른 하나를 선택할 수 있습니다 `connection.GetDatabase(dbid)` 여기서 `dbid` 는 사이의 숫자 `0` 및 `databases - 1`합니다. |
| `maxclients` |Hello 가격 책정 계층에 따라 달라 집니다<sup>2</sup> |이 hello 동일 hello에 허용 되는 연결 된 클라이언트의 최대 수 시간입니다. Hello도 도달 하면 Redis가 닫습니다 모든 hello 새 연결이 'max number of clients reached' 오류를 반환 합니다. |
| `maxmemory-policy` |`volatile-lru` |Redis 어떤 tooremove를 선택 하는 방법에 대 한 최대 메모리 정책은 hello 설정 때 `maxmemory` (hello 캐시 hello 캐시를 만들 때 선택한 기능 hello 크기)에 도달 했습니다. Azure Redis Cache hello 기본 설정은 `volatile-lru`, LRU 알고리즘을 사용 하 여 설정 하는 만료 된 hello 키를 제거 합니다. 이 설정은 hello Azure 포털에서에서 구성할 수 있습니다. 자세한 내용은 [메모리 정책](#memory-policies)을 참조하세요. |
| `maxmemory-samples` |3 |toosave 메모리, LRU 및 최소 TTL 알고리즘은 정확한 알고리즘이 아니라 근사치로 계산 된 알고리즘입니다. 기본적으로 Redis 검사 세 개의 키 및 선택 hello 하나 덜 최근에 사용 되었습니다. |
| `lua-time-limit` |5, 000 |밀리초 단위의 Lua 스크립트 최대 실행 시간입니다. Hello 최대 실행 시간에 도달 하면 Redis는 스크립트가 허용 된 시간, 최대 hello 후 실행 중인 이며 tooreply tooqueries 오류가 발생 하 여 시작을 기록 합니다. |
| `lua-event-limit` |500 |스크립트 이벤트 큐의 최대 크기 |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |hello 클라이언트 출력 버퍼 제한을 사용 될 수 있습니다 (일반적인 이유는 Pub/Sub 클라이언트 메시지를 hello 게시자에서 생성 하는 것에 가능한 한 빨리 사용할 수 없습니다) 몇 가지 이유로 적당히 빠르게 hello 서버에서 데이터를 읽고 있지 않은 클라이언트의 tooforce 연결 해제를 사용 합니다. 자세한 내용은 [http://redis.io/topics/clients](http://redis.io/topics/clients)를 참조하세요. |

<a name="databases"></a>
<sup>1</sup>hello 제한을 `databases` 각 Azure Redis Cache 가격 책정 계층에 대 한 다른 하며 캐시를 만들 때 설정할 수 있습니다. 되지 않은 경우 `databases` 설정이 지정 캐시 만들기 중 hello 기본값은 16입니다.

* 기본 및 표준 캐시
  * C0 (250MB) 캐시-too16 데이터베이스를
  * C1 too16 데이터베이스를 캐시-(1GB)
  * C2 too16 데이터베이스를 캐시-(2.5 g B)
  * C3 too16 데이터베이스를 캐시-(6 GB)
  * C4 too32 데이터베이스를 캐시-(13 GB)
  * C5 (26GB) 캐시-too48 데이터베이스를
  * C6 too64 데이터베이스를 캐시-(53 GB)
* 프리미엄 캐시
  * P1 (6GB-60 GB)-too16 데이터베이스를
  * P2 (13 GB-130 GB)-too32 데이터베이스를
  * Too48 데이터베이스를 P3 (26GB-260 GB)-
  * Too64 데이터베이스를 P4 (53GB-530 GB)-
  * Redis 클러스터 사용-와 모든 프리미엄 캐시 Redis 클러스터만 지원 0 데이터베이스의 사용 하므로 hello `databases` Redis 클러스터를 사용할 수 있는 모든 프리미엄 캐시는 효과적으로 1과 hello에 대 한 한계 [선택](http://redis.io/commands/select) 명령을 허용 하지 않습니다. 자세한 내용은 참조 [필요 합니까 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

데이터베이스에 대한 자세한 내용은 [Redis 데이터베이스란?](cache-faq.md#what-are-redis-databases)을 참조하세요.

> [!NOTE]
> hello `databases` 캐시 만들기 중에 구성 하 고 PowerShell, CLI 또는 기타 관리 클라이언트를 사용 하 여만 설정할 수 있습니다. PowerShell을 사용하여 캐시를 만드는 동안 `databases` 를 구성하는 예제는 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)를 참조하세요.
> 
> 

<a name="maxclients"></a>
<sup>2</sup>`maxclients`는 Azure Redis Cache 가격 책정 계층마다 다릅니다.

* 기본 및 표준 캐시
  * C0 (250MB) 캐시-too256 연결을
  * C1 too1 (1GB) 캐시-, 000 연결
  * C2-too2 (2.5 g B) 캐시, 000 연결
  * C3 too5 (6GB) 캐시-, 000 연결
  * C4 too10 13 4GB 캐시-, 000 연결
  * C 5-too15 (26GB) 캐시, 000 연결
  * C 6-too20 (53GB) 캐시, 000 연결
* 프리미엄 캐시
  * Too7, 500 개의 연결을 P1 (6GB-60 GB)-
  * P2 (13 GB-130 GB)-too15, 000 연결 구성
  * Too30, 000 연결 구성 (26GB-260 GB)-P3
  * Too40, 000 연결을 P4 (53GB-530 GB)-

> [!NOTE]
> 각 캐시 크기를 허용 하지만 *최대* 연결의 특정 수, 각 연결 tooRedis 오버 헤드가 연결 되어 있습니다. 이러한 오버헤드의 예로 TLS/SSL 암호화의 결과인 CPU 및 메모리 사용량이 있습니다. 특정된 캐시 크기에 대 한 최대 연결 제한 hello 부하가 적은 캐시를 가정합니다. 하는 경우 연결 오버 헤드가에서 로드할 *플러스* hello 시스템에 대 한 용량을 초과 하는 클라이언트 작업에서의 로드, hello 현재 캐시 크기에 대 한 hello 연결 제한을 초과한 경우에 hello 캐시 용량 문제가 발생할 수 있습니다.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Azure Redis Cache에서 지원되지 않는 Redis 명령
> [!IMPORTANT]
> 구성 및 관리 Azure Redis 캐시 인스턴스의 Microsoft에서 관리 하므로 hello 다음 명령은 사용할 수 없습니다. Tooinvoke 시도 하면 너무 유사한 오류 메시지가 나타납니다에`"(error) ERR unknown command"`합니다.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * 저장
> * SHUTDOWN
> * SLAVEOF
> * 클러스터 - 클러스트 쓰기 명령은 비활성화되지만, 읽기 전용 클러스터 명령은 허용됩니다.
> 
> 

Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.

## <a name="redis-console"></a>Redis 콘솔
안전 하 게 명령을 실행할 수 있습니다 hello를 사용 하 여 tooyour Azure Redis Cache 인스턴스 **Redis 콘솔**, hello 모든 캐시 계층에 대해 Azure 포털에서에서 사용할 수 있습니다.

> [!IMPORTANT]
> - hello Redis 콘솔에서 작동 하지 않습니다 [VNET](cache-how-to-premium-vnet.md)합니다. 캐시는 VNET의 일부 이면 hello 캐시 hello VNET에서에서 클라이언트에만 액세스할 수 있습니다. Redis 콘솔을 벗어난 hello VNET 로컬 브라우저에서 실행 되므로 tooyour 캐시를 연결할 수 없는 합니다.
> - 일부 Redis 명령은 Azure Redis Cache에서 지원되지 않습니다. Azure Redis Cache에 사용 되지 않는 Redis 명령 목록이 이전 hello 참조 [Azure Redis Cache에서 지원 되지 않는 명령 Redis](#redis-commands-not-supported-in-azure-redis-cache) 섹션. Redis 명령에 대한 자세한 내용은 [http://redis.io/commands](http://redis.io/commands)를 참조하세요.
> 
> 

tooaccess hello Redis 콘솔 클릭 **콘솔** hello에서 **Redis Cache** 블레이드입니다.

![Redis 콘솔](./media/cache-configure/redis-console-menu.png)

캐시 인스턴스에 대해 tooissue 명령을 단순히 형식 hello 명령 hello 콘솔에 원하는입니다.

![Redis 콘솔](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>premium Redis 콘솔 hello를 사용 하 여 캐시 클러스터

캐시 클러스터는 premium hello Redis 콘솔을 사용 하 여 명령을 tooa 단일 분할 영역 hello 캐시의 발급할 수 있습니다. 먼저 tooissue 명령 tooa 특정 분할 hello 분할 선택에서 클릭 하 여 toohello 원하는 분할 영역을 연결 합니다.

![Redis 콘솔](./media/cache-configure/redis-console-premium-cluster.png)

Tooaccess 연결 된 분할 hello 보다 다른 분할 영역에 저장 된 키를 만들려고 하면 메시지의 뒤에 오류 메시지와 비슷한 toohello를 나타납니다.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

Hello 이전 예제에서는 분할 영역 1 hello 선택한 분할 영역에는 있지만 `myKey` hello에 표시 된 대로 0, 분할 된 데이터베이스에 있는 `(shard 0)` hello 오류 메시지의 부분입니다. 이 예제에서는 tooaccess `myKey`선택 합니다 shard 코드 조각 선택기 및 문제 원하는 hello 명령 hello 0 분할 된 데이터베이스를 사용 하 여 합니다.


## <a name="move-your-cache-tooa-new-subscription"></a>캐시 tooa 새 구독 이동
클릭 하 여 캐시 tooa 새 구독을 이동할 수 있습니다 **이동**합니다.

![Redis Cache 이동](./media/cache-configure/redis-cache-move.png)

하나의 리소스 그룹 tooanother 및 구독을 하나 tooanother에서 리소스를 이동 하는 방법은 참조 하십시오. [리소스 toonew 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.

## <a name="next-steps"></a>다음 단계
* Redis 명령을 사용하는 방법은 [어떻게 Redis 명령을 실행할 수 있나요?](cache-faq.md#how-can-i-run-redis-commands)를 참조하세요.


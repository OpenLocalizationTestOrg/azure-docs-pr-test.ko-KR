---
title: Azure Redis Cache aaaHow toomonitor | Microsoft Docs
description: "자세한 방법을 toomonitor hello 상태와 성능을 Azure Redis Cache 인스턴스"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Azure Redis 캐시 하는 toomonitor 방법
Azure Redis Cache를 사용 하 여 [Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide 캐시 인스턴스를 모니터링 하는 여러 가지 옵션입니다. 볼 메트릭, 메트릭 차트 toohello 시작 보드에 고정, 모니터링 차트의 hello 날짜 및 시간 범위를 사용자 지정, 추가 및 hello 차트에서 메트릭을 제거 있고 특정 조건이 충족 될 때 경고를 설정 합니다. 이러한 도구는 하면 toomonitor hello 상태 Azure Redis 캐시 인스턴스를 사용 하도록 설정 하 고 캐싱 응용 프로그램을 관리 하는 데 도움이 됩니다.

메트릭을 사용 하 여 Azure Redis Cache 인스턴스는 수집에 대 한 hello Redis [정보](http://redis.io/commands/info) 30 일 동안 자동으로 저장 및 분 당 2 배 정도 빨라질 명령 (참조 [캐시 메트릭 내보내기](#export-cache-metrics) tooconfigure는 다른 보존 정책을) hello 메트릭 차트에 표시 되 고 경고 규칙에 따라 평가 될 수 있도록 합니다. 각 캐시 메트릭에 사용 되는 hello 다른 정보 값에 대 한 자세한 내용은 참조 [사용 가능한 메트릭 및 보고 간격](#available-metrics-and-reporting-intervals)합니다.

<a name="view-cache-metrics"></a>

tooview 캐시 메트릭 [찾아보기](cache-configure.md#configure-redis-cache-settings) hello의 tooyour 캐시 인스턴스에 [Azure 포털](https://portal.azure.com)합니다.  Hello에 몇 가지 기본 제공 차트를 제공 하는 azure Redis 캐시 **개요** 블레이드 및 hello **메트릭 Redis** 블레이드입니다. 각 차트는 메트릭을 추가 또는 제거한 hello 보고 간격을 변경 하 여 사용자 지정할 수 있습니다.

![Redis 메트릭](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>미리 구성된 메트릭 차트 보기

hello **개요** 블레이드는 hello 미리 구성 된 모니터링 차트를 수행 합니다.

* [모니터링 차트](#monitoring-charts)
* [사용 현황 차트](#usage-charts)

### <a name="monitoring-charts"></a>모니터링 차트
hello **모니터링** hello 섹션인 **개요** 블레이드는 **적중 및 누락 수**, **가져오고 설정**, **연결**, 및 **총 명령** 차트입니다.

![모니터링 차트](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>사용 현황 차트
hello **사용량** hello 섹션인 **개요** 블레이드는 **Redis 서버 로드가**, **메모리 사용량**, **네트워크 대역폭** , 및 **CPU 사용량** , 차트 및 hello 표시 **가격 책정 계층** hello 캐시 인스턴스에 대 한 합니다.

![사용 현황 차트](./media/cache-how-to-monitor/redis-cache-usage-part.png)

hello **가격 책정 계층** 표시 hello 캐시 가격 책정 계층을 지 및도 사용할 수 있습니다[배율](cache-how-to-scale.md) 가격 책정 계층을 서로 다른 캐시 tooa hello 합니다.

## <a name="view-metrics-with-azure-monitor"></a>Azure Monitor의 메트릭 보기
tooview Redis 메트릭 및 Azure 모니터를 사용 하는 사용자 지정 차트를 만들 클릭 **메트릭** hello에서 **리소스 메뉴**, 원하는 hello 메트릭을 사용 하 여, 간격, 차트 종류를 보고 차트를 사용자 지정 하 고 및 더 많은 합니다.

![Redis 메트릭](./media/cache-how-to-monitor/redis-cache-monitor.png)

Azure Monitor에서 메트릭을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure의 메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md)를 참조하세요.

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>캐시 메트릭 내보내기
기본적으로 Azure Monitor의 캐시 메트릭은 [30일 동안 저장](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)되었다가 삭제됩니다. toopersist 수 30 일 보다 오래 하면 캐시 메트릭이 [저장소 계정을 지정](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) 지정는 **보존 (일)** 캐시 메트릭에 대 한 정책입니다. 

tooconfigure 캐시 메트릭에 대 한 저장소 계정:

1. 클릭 **진단** hello에서 **리소스 메뉴** hello에 **Redis Cache** 블레이드입니다.
2. **설정**을 클릭합니다.
3. 확인 **tooa 저장소 계정 보관**합니다.
4. Toostore hello 캐시 메트릭을에 hello 저장소 계정을 선택 합니다.
5. Hello 확인 **1 분** 확인란을 선택 하 고 지정는 **보존 (일)** 정책입니다. 원하는 대로 보존 정책을 tooapply 원하는 하지 않으며 데이터를 영원히 유지 하는 경우 설정 **보존 (일)** 너무**0**합니다.
6. **Save**를 클릭합니다.

![Redis 진단](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>추가 tooarchiving 프로그램 캐시 메트릭을 toostorage 수도 있습니다 [스트리밍할 tooan 이벤트 허브 또는 tooLog 분석 보내기](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)합니다.
>
>

tooaccess 메트릭, hello이이 문서에 설명 된 대로 Azure 포털에서 볼 수 있습니다, 그리고도 액세스할 수 hello를 사용 하 여 [Azure 모니터 메트릭 REST API](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api)합니다.

> [!NOTE]
> 저장소 계정을 변경 하면 hello hello 이전에 구성 된 저장소 계정의 데이터를에서 계속 다운로드를 사용할 수 있지만 hello Azure 포털에에서 표시 되지 않습니다.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>사용 가능한 메트릭 및 보고 간격
캐시 메트릭은 **지난 시간**, **오늘**, **지난 주** 및 **사용자 지정**을 포함한 몇 가지 보고 간격을 사용하여 보고됩니다. hello **메트릭을** 블레이드 각 메트릭 차트에 대 한 hello 차트에서 각 메트릭에 대 한 hello 평균, 최소 및 최대 값을 표시 하 고 일부 메트릭을 보고 간격 hello에 대 한 합계를 표시 합니다. 

각 메트릭은 두 가지 버전을 포함합니다. 메트릭을 하나를 사용 하는 캐시 및 hello 전체 캐시에 대 한 성능 측정 [클러스터링](cache-how-to-premium-clustering.md), 두 번째 버전을 포함 하는 hello 메트릭의 `(Shard 0-9)` 캐시에 단일 분할 영역에 대 한 hello 이름 측정값 성능이 합니다. 예를 들어 분할 4 개가 캐시가 `Cache Hits` hello 전체 캐시에 대 한 적중의 총 양 hello 및 `Cache Hits (Shard 3)` hello 캐시의 해당 분할에 대 한 바로 hello 적중 됩니다.

> [!NOTE]
> Hello 캐시 경우에 연결 된 활성 클라이언트 응용 프로그램이 없는 유휴 상태, 연결 된 클라이언트, 메모리 사용량, 수행 되는 작업 등의 일부 캐시 활동이 나타날 수 있습니다. 이 작업은 Azure Redis Cache 인스턴스 hello 작업 중 정상입니다.
> 
> 

| 메트릭 | 설명 |
| --- | --- |
| 캐시 적중 |hello hello 지정한 보고 간격 동안 성공한 키 조회 수입니다. 너무 매핑됩니다`keyspace_hits` hello Redis에서에서 [정보](http://redis.io/commands/info) 명령입니다. |
| 캐시 누락 |hello hello 지정한 보고 간격 동안 실패 한 키 조회 수입니다. 너무 매핑됩니다`keyspace_misses` hello 정보 Redis 명령에서에서 합니다. 캐시 누락 않습니다 해 서 반드시 hello 캐시와 문제가 있습니다. 예를 들어 hello 캐시 배제 프로그래밍 패턴을 사용할 경우 응용 프로그램 검색 첫 번째 항목에 대 한 hello 캐시 합니다. Hello 항목이 없는 경우 (캐시 누락), hello hello 데이터베이스에서 검색 된 항목과 toohello 캐시 다음에 추가 합니다. 캐시 누락은 캐시 배제 프로그래밍 패턴 hello에 대 한 일반적인 동작입니다. Hello 캐시 누락 수가 예상 보다 높은 경우 채우고 hello 캐시에서 읽고 있는 hello 응용 프로그램 논리를 검사 합니다. Toomemory 압력 때문 hello 캐시에서 항목이 제거 되 고은 다음 캐시 누락 수 있지만 메모리 압력에 대 한 더 나은 메트릭 toomonitor 것 경우 `Used Memory` 또는 `Evicted Keys`합니다. |
| 연결된 클라이언트 |클라이언트 hello 지정한 보고 간격 동안 연결 toohello 캐시 hello 수입니다. 너무 매핑됩니다`connected_clients` hello 정보 Redis 명령에서에서 합니다. 한 번 hello [연결 제한](cache-configure.md#default-redis-server-configuration) 에 도달 하면 이후 연결 시도가 toohello 캐시 실패 합니다. 하 활성 클라이언트 응용 프로그램이 없는 경우에 있을 수 있습니다 toointernal 프로세스 및 연결 때문에 연결 된 클라이언트의 몇 가지 인스턴스여야 합니다. |
| 제거된 키 |hello hello 중 hello 캐시에서 제거 하는 항목 수가 지정 된 보고 간격 due toohello `maxmemory` 제한 합니다. 너무 매핑됩니다`evicted_keys` hello 정보 Redis 명령에서에서 합니다. |
| 만료된 키 |항목 수가 hello hello 지정한 보고 간격 동안 hello 캐시에서 만료 되었습니다. 이 값이 너무 매핑할`expired_keys` hello 정보 Redis 명령에서에서 합니다. |
| 전체 키  | hello hello 이전 보고 기간 중 hello 캐시에 있는 키의 최대 수입니다. 너무 매핑됩니다`keyspace` hello 정보 Redis 명령에서에서 합니다. 클러스터링을 사용 하 고, 캐시에 대 한 메트릭 시스템의 기반이 되는 hello tooa 제한인 인해 총 키 hello의 hello 보고 간격 동안 hello 최대 키 수 있었던 hello 분할 키의 최대 수를 반환 합니다.  |
| 가져오기 |hello hello 지정한 보고 간격 동안 hello 캐시에서 get 작업 수입니다. 이 값은 모든 명령을 hello Redis 정보에서에서 hello 다음의 hello 합계 값: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, 및 `cmdstat_getrange`, 캐시 적중 횟수의 합계와 동일한 toohello 및 및 hello 보고 간격 동안 누락입니다. |
| Redis 서버 부하 |주기는 hello에서 Redis 서버는 사용 중 처리 및 메시지에 대 한 유휴 상태를 대기 하지 않는 hello 비율입니다. 이 카운터가 100 hello Redis 서버 성능 최대값에 도달 하 고 처리할 수 없습니다. CPU hello 있음을 의미 하는 경우 하나 더 빠르게 작동 합니다. Redis 서버 로드가 표시 되는 경우 다음 보게 hello 클라이언트의 시간 제한 예외. 이 경우 강화나 여러 캐시로의 데이터 분할을 고려해야 합니다. |
| 설정 |hello 중 집합 작업 toohello 캐시 hello 수는 보고 간격을 지정합니다. 이 값은 모든 명령을 hello Redis 정보에서에서 hello 다음의 hello 합계 값: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` 및 `cmdstat_setnx`합니다. |
| 총 작업 |hello hello 동안 hello 캐시 서버에서 처리 되는 명령의 총 수는 보고 간격을 지정 합니다. 이 값이 너무 매핑할`total_commands_processed` hello 정보 Redis 명령에서에서 합니다. Azure Redis Cache pub/sub에 순수 하 게 사용 되는 경우는 있을 대 한 메트릭은 `Cache Hits`, `Cache Misses`, `Gets`, 또는 `Sets`, 이지만 `Total Operations` pub/sub 작업에 대 한 hello 캐시 사용량을 반영 하는 메트릭을 합니다. |
| 사용된 메모리 |hello hello 중 mb에서 hello 캐시에 키/값 쌍에 대해 사용 하는 캐시 메모리 양을 보고 간격을 지정 합니다. 이 값이 너무 매핑할`used_memory` hello 정보 Redis 명령에서에서 합니다. 메타데이터 또는 조각화를 포함하지 않습니다. |
| 사용된 메모리 RSS |캐시 메모리 (MB) 사용 하 여 hello 지정한 보고 간격 동안, 조각화 및 메타 데이터를 포함 하 여 hello 양입니다. 이 값이 너무 매핑할`used_memory_rss` hello 정보 Redis 명령에서에서 합니다. |
| CPU |hello hello Azure Redis Cache 서버의 백분율 동안 cpu hello 보고 간격을 지정 합니다. 이 값이 매핑할 toohello 운영 체제 `\Processor(_Total)\% Processor Time` 성능 카운터입니다. |
| 캐시 읽기 |hello 동안 (m B/초) 초당 메가바이트 단위로 hello 캐시에서 읽은 데이터 hello 공간은 보고 간격을 지정 합니다. 이 값은 하지 특정 Redis를 hello 캐시를 호스트 하는 hello 가상 컴퓨터를 지 원하는 hello 네트워크 인터페이스 카드에서 파생 됩니다. **이 값이이 캐시에서 사용 되는 toohello 네트워크 대역폭을 해당 합니다. 서버 쪽 네트워크 대역폭 제한에 대 한 경고를 tooset 하려는 경우 다음 사용 하 여 만들이 `Cache Read` 카운터입니다. 참조 [이 테이블](cache-faq.md#cache-performance) 다양 한 캐시 가격 책정 계층 및 크기에 대 한 대역폭 제한을 관찰 된 hello에 대 한 합니다.** |
| 캐시 쓰기 |기록한 toohello 캐시 메가바이트에서 (MB/s) hello 지정한 보고 간격 동안 데이터의 양을 hello 합니다. 이 값은 하지 특정 Redis를 hello 캐시를 호스트 하는 hello 가상 컴퓨터를 지 원하는 hello 네트워크 인터페이스 카드에서 파생 됩니다. 이 값은 toohello 캐시 hello 클라이언트에서 전송 된 데이터의 네트워크 대역폭 toohello 해당 합니다. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>경고
메트릭 및 활동 로그를 기반으로 하는 tooreceive 경고를 구성할 수 있습니다. Azure 모니터 표시할 때을 다음 경고 toodo hello tooconfigure가 있습니다.

* 전자 메일 알림 보내기
* 웹후크 호출
* Azure 논리 앱 호출

캐시에 대 한 경고 규칙 tooconfigure 클릭 **규칙 경고** hello에서 **리소스 메뉴**합니다.

![모니터링](./media/cache-how-to-monitor/redis-cache-monitoring.png)

경고 구성 및 사용에 대한 자세한 내용은 [경고 개요](../monitoring-and-diagnostics/insights-alerts-portal.md)를 참조하세요.

## <a name="activity-logs"></a>활동 로그
활동 로그에서 Azure Redis 캐시 인스턴스에 수행 된 hello 작업에 대 한 정보를 제공 합니다. 이전에는 이러한 로그를 "감사 로그" 또는 "작업 로그"라고도 했습니다. 작업 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE)에서 Azure Redis Cache 인스턴스 사용에 대 한 합니다. 

> [!NOTE]
> 활동 로그에는 읽기(GET) 작업은 포함되지 않습니다.
>
>

캐시에 대 한 활동 로그 tooview 클릭 **활동 로그** hello에서 **리소스 메뉴**합니다.

활동 로그에 대 한 자세한 내용은 참조 [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)합니다.












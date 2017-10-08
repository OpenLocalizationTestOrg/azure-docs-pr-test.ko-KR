---
title: Azure Redis Cache aaaHow tootroubleshoot | Microsoft Docs
description: "Azure Redis 캐시 tooresolve 공통 발급 하는 방법에 대해 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Azure Redis 캐시 하는 tootroubleshoot 방법
이 문서에서는 Azure Redis Cache 문제 범주에 따라 hello 문제 해결 지침을 제공 합니다.

* [클라이언트 쪽 문제 해결](#client-side-troubleshooting) -이 섹션에서는 확인 지침을 제공 하 고 tooAzure Redis Cache를 연결 하는 hello 응용 프로그램에 의해 발생 한 문제를 해결 합니다.
* [서버 쪽 문제 해결](#server-side-troubleshooting) -이 섹션에서는 확인 지침을 제공 하 고 Azure Redis Cache 서버 쪽 hello에 발생 문제를 해결 합니다.
* [StackExchange.Redis의 시간 제한 예외](#stackexchangeredis-timeout-exceptions) -이 섹션에서는 hello StackExchange.Redis 클라이언트를 사용 하는 경우 문제 해결에 정보를 제공 합니다.

> [!NOTE]
> 몇 가지 문제 해결 단계는이 가이드의 hello toorun Redis 명령 하 고 다양 한 성능 메트릭을 모니터링할 지침이 포함 됩니다. 자세한 내용 및 지침에 대 한 hello에 hello 문서를 참조 [추가 정보](#additional-information) 섹션.
> 
> 

## <a name="client-side-troubleshooting"></a>클라이언트 쪽 문제 해결
이 섹션에서는 hello 클라이언트 응용 프로그램에 대 한 조건으로 인해 발생 하는 문제 해결을 설명 합니다.

* [클라이언트 hello에 메모리가 중](#memory-pressure-on-the-client)
* [트래픽 폭주](#burst-of-traffic)
* [클라이언트의 높은 CPU 사용량](#high-client-cpu-usage)
* [클라이언트 쪽 대역폭 초과](#client-side-bandwidth-exceeded)
* [큰 요청/응답 크기](#large-requestresponse-size)
* [Redis에서 발생 했습니다 toomy 데이터?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>클라이언트 hello에 메모리가 중
#### <a name="problem"></a>문제
Hello가 클라이언트 컴퓨터에 메모리가 중 tooall 유형의 지연 없이 hello Redis 인스턴스에서 보낸 데이터의 처리를 지연 시킬 수 있는 성능 문제를 안내 합니다. 메모리가 중에 도달 하면 hello 시스템은 일반적으로 디스크에 있는 실제 메모리 toovirtual 메모리에서 toopage 데이터에 있습니다. 이 *페이지 오류가* 원인을 아래로 크게 시스템 tooslow을 hello 합니다.

#### <a name="measurement"></a>측정
1. 사용 가능한 메모리를 초과 하지 않는 컴퓨터 toomake에서 메모리 사용량을 모니터링 합니다. 
2. 모니터 hello `Page Faults/Sec` 성능 카운터입니다. 대부분의 시스템은 정상 작동을 하는 중에도 약간의 페이지 폴트가 있으므로 시간 제한에 해당하는 이 페이지 폴트 성능 카운터에서의 급증을 확인합니다.

#### <a name="resolution"></a>해결 방법
메모리 사용량 패턴 tooreduce 메모리 consuption 자세히 검토 하거나 클라이언트 tooa 큰 클라이언트 메모리가 더 많은 VM 크기를 업그레이드 합니다.

### <a name="burst-of-traffic"></a>트래픽 폭주
#### <a name="problem"></a>문제
트래픽 급증 나쁨 함께 `ThreadPool` 설정을 hello Redis 서버에서 보낸 이미 있지만 hello 클라이언트 쪽에서 아직 사용 중인 데이터 처리에 지연이 발생할 수 있습니다.

#### <a name="measurement"></a>측정
[다음과 같은](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs) 코드를 사용할 때 `ThreadPool` 통계가 시간에 따라 어떻게 바뀌는지 모니터링합니다. Hello을 살펴볼 수도 있습니다 `TimeoutException` StackExchange.Redis의 메시지입니다. 다음은 예제입니다:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

Hello 메시지 위에,에서 주목할 만한 몇 가지 문제도 있습니다.

1. 에 해당 hello 확인 `IOCP` 섹션과 hello `WORKER` 있는 섹션은 `Busy` hello 보다 큰 값을 `Min` 값입니다. 이는 `ThreadPool` 설정이 조정을 필요로 한다는 의미입니다.
2. 또한 `in: 64221`도 볼 수 있습니다: 64211 바이트 hello 커널 소켓 계층에서 받은 하지만 hello 응용 프로그램 (예: StackExchange.Redis)에서 아직 읽지 않은 나타냅니다. 이 일반적으로 응용 프로그램 되지에서 데이터를 읽는 hello 네트워크 hello 서버 tooyou 보내기는 최대한 빨리 의미 합니다.

#### <a name="resolution"></a>해결 방법
구성 프로그램 [스레드 풀 설정](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake 스레드 풀에서 신속 하 게 수직 됩니다 있는지 시나리오를 전환 합니다.

### <a name="high-client-cpu-usage"></a>클라이언트의 높은 CPU 사용량
#### <a name="problem"></a>문제
Hello 클라이언트에서 CPU 사용량이 hello 시스템 하 고 요청 받았습니다 tooperform hello 작업을 계속할 수를 나타냅니다. 즉, Redis hello 응답을 매우 신속 하 게 전송 하는 경우에 해당 hello 클라이언트 tooprocess Redis의 응답을 적시에 실패할 수 있습니다.

#### <a name="measurement"></a>측정
Hello 또는 hello Azure 포털을 통해 시스템 넓은 CPU 사용량 모니터 hello 성능 카운터를 연결 합니다. 주의 해야 하지 toomonitor *프로세스* CPU 단일 프로세스에서 CPU 사용량이 낮은 있을 수 있으므로 hello 동일한 시간 전반적인 시스템 CPU 커질 수 있습니다. CPU 사용량에서 제한 시간에 해당 하는 급증을 확인합니다. 높은 CPU의 결과로 나타날 높은 `in: XXX` 값 `TimeoutException` hello에 설명 된 대로 오류 메시지를 [트래픽의 버스트](#burst-of-traffic) 섹션.

> [!NOTE]
> StackExchange.Redis 1.1.603 hello 나중 작성과 `local-cpu` 에 메트릭 `TimeoutException` 오류 메시지입니다. 최신 버전의 hello hello를 사용 하 여 알아보기 위한 [StackExchange.Redis NuGet 패키지](https://www.nuget.org/packages/StackExchange.Redis/)합니다. 지속적으로 되 고 버그에 없는 고정 hello 코드 toomake 것 보다 강력한 tootimeouts hello 최신 버전이 하는 것이 중요 합니다.
> 
> 

#### <a name="resolution"></a>해결 방법
CPU 용량이 더 큰 tooa 더 큰 VM 크기를 업그레이드 하거나 CPU 스파이크 원인을 확인 합니다. 

### <a name="client-side-bandwidth-exceeded"></a>클라이언트 쪽 대역폭 초과
#### <a name="problem"></a>문제
크기가 다른 클라이언트 컴퓨터는 어느 정도의 네트워크 대역폭을 사용할 수 있는지에 제한이 있습니다. 클라이언트 hello 초과 하는 경우 사용 가능한 대역폭, hello 다음 데이터 처리 되지 않습니다 hello 클라이언트 쪽에서 hello 서버에서 보내기는 신속 하 게 합니다. Tootimeouts를 발생할 수 있습니다.

#### <a name="measurement"></a>측정
[다음과 같은](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs)코드를 사용할 때 대역폭 사용량이 시간에 따라 어떻게 바뀌는지 모니터링합니다. 이 코드는 (Azure 웹 사이트와 같이) 권한이 제한된 일부 환경에서 성공적으로 실행되지 않을 수도 있습니다.

#### <a name="resolution"></a>해결 방법
클라이언트 VM 크기를 늘리거나 네트워크 대역폭 사용량을 줄입니다.

### <a name="large-requestresponse-size"></a>큰 요청/응답 크기
#### <a name="problem"></a>문제
큰 요청/응답으로 시간 초과가 발생할 수 있습니다. 예를 들어 클라이언트에 구성된 시간 제한 값이 1초라고 가정합시다. 응용 프로그램이 (동일한 실제 네트워크 연결을 사용하여)  'A' 및 'B') hello에서 동시 (동일한 실제 네트워크 연결 hello를 사용 하 여). 대부분 클라이언트는 같은 'A' 및 'B' 모두 요청이 전송 되는 hello 와이어 toohello 서버 하나에서 hello 후 다른 hello 응답을 기다리지 않고 "파이프라이닝" 요청을 지원 합니다. hello 서버 보낼 hello 응답을 다시 hello에 동일 주문 합니다. 응답 'A' 크면 것 만큼 수 소요 되는 대부분의 후속 요청에 대 한 hello 제한 시간입니다. 

다음 예제는 hello이이 시나리오를 보여 줍니다. 이 시나리오에서는 'A' 및 'B'는 보낸 요청 신속 하 게 hello 서버 응답 'A' 및 'B'를 신속 하 게 보내기 시작 되기는 하지만 데이터 전송 시간 때문에 'B' 뒤에 갇 hello 서버 응답 신속 하 게 하는 경우에 다른 요청 및 제한 시간이 초과 hello 합니다.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>측정
이 어려운 하나 toomeasure입니다. 기본적으로 tooinstrument 클라이언트 코드 tootrack 큰 요청 및 응답에 있어야 합니다. 

#### <a name="resolution"></a>해결 방법
1. Redis는 몇 개의 큰 값보다는 많은 수의 작은 값에 대해 최적화됩니다. hello는 솔루션은 toobreak 관련된 더 작은 값으로 데이터를 기본 설정입니다. Hello 참조 [redis 용 hello 이상적인 값 크기 범위를 란? 100KB는 너무 큽니다?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)게시물을 참조하세요.
2. Hello 크기 늘리기 (클라이언트 및 Redis 캐시 서버)에 대해 VM의 tooget 더 높은 대역폭 기능, 데이터를 줄이면 더 큰 응답에 대 한 시간을 전송 합니다. 해당 더 많은 대역폭에 대 한 가져오는 hello 서버에만 또는 있는 것이 아니라 hello 클라이언트 충분할 수도 있습니다. 대역폭 사용량을 측정 하 고 현재 VM의 hello 크기의 toohello 기능을 비교 합니다.
3. Hello 수를 증가 `ConnectionMultiplexer` 서로 다른 연결을 통해 사용 및 라운드 로빈 요청 개체입니다.

### <a name="what-happened-toomy-data-in-redis"></a>Redis에서 발생 했습니다 toomy 데이터?
#### <a name="problem"></a>문제
예상 특정 데이터 toobe Azure Redis Cache 인스턴스 내에 있지만 toobe 발생 하지 않은 것입니다.

#### <a name="resolution"></a>해결 방법
참조 [Redis에서 발생 했습니다 toomy 데이터?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) 가능한 원인 및 해결 방법에 대 한 합니다.

## <a name="server-side-troubleshooting"></a>서버 쪽 문제 해결
이 섹션에서는 hello 캐시 서버에 대 한 조건으로 인해 발생 하는 문제 해결을 설명 합니다.

* [Hello 서버에서 메모리가 중](#memory-pressure-on-the-server)
* [높은 CPU 사용량 / 서버 부하](#high-cpu-usage-server-load)
* [서버 쪽 대역폭 초과](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Hello 서버에서 메모리가 중
#### <a name="problem"></a>문제
Hello 서버 쪽에서 메모리가 중 tooall 종류의 요청을 처리를 지연 시킬 수 있는 성능 문제를 안내 합니다. 메모리가 중에 도달 하면 hello 시스템은 일반적으로 디스크에 있는 실제 메모리 toovirtual 메모리에서 toopage 데이터에 있습니다. 이 *페이지 오류가* 원인을 아래로 크게 시스템 tooslow을 hello 합니다. 이 메모리 부족의 몇 가지 가능한 원인은 다음과 같습니다. 

1. 데이터로 hello 캐시 toofull 용량을 입력 했습니다. 
2. Redis 높은 메모리 조각화-큰 개체를 저장 하 여 가장 자주 발생 보고 (작은 개체-참조 hello에 대 한 최적화 된 Redis [redis 용 hello 이상적인 값 크기 범위를 란? 100KB는 너무 큽니다?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)게시물을 참조하세요) 

#### <a name="measurement"></a>측정
Redis는 이 문제를 식별하는 데 도움이 되는 두 개의 메트릭을 노출합니다. hello 먼저가 `used_memory` hello 다른 이며 `used_memory_rss`합니다. [이러한 메트릭은](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) hello Azure 포털 또는 hello를 통해 사용할 수 있는 [Redis 정보](http://redis.io/commands/info) 명령입니다.

#### <a name="resolution"></a>해결 방법
변경할 수 있는 toohelp 유지 메모리 사용량이 정상 몇 가지 가능한 변경 사항이 있습니다.

1. [메모리 정책을 구성](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 하고 키에 만료 시간을 설정합니다. 조각화가 있을 경우 이것으로는 부족할 수 있습니다.
2. [Maxmemory 예약 값 구성](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 충분히 큰 toocompensate 즉 메모리 조각화 합니다.
3. 크게 캐시된 개체를 더 작은 관련 개체로 분할합니다.
4. [배율](cache-how-to-scale.md) tooa 더 큰 캐시 크기.
5. 사용 하는 경우는 [Redis 클러스터를 사용할 수 있는 프리미엄 캐시](cache-how-to-premium-clustering.md) 할 수 있습니다 [hello 분할 영역 수를 증가](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache)합니다.

### <a name="high-cpu-usage--server-load"></a>높은 CPU 사용량 / 서버 부하
#### <a name="problem"></a>문제
CPU 사용량이 Redis hello 응답을 매우 신속 하 게 전송 하는 경우에 hello 클라이언트 쪽 tooprocess 시기 적절 하 게에서 Redis 로부터 응답에 실패할 수 있습니다는 의미할 수 있습니다.

#### <a name="measurement"></a>측정
Hello 또는 hello Azure 포털을 통해 시스템 넓은 CPU 사용량 모니터 hello 성능 카운터를 연결 합니다. 주의 해야 하지 toomonitor *프로세스* CPU 단일 프로세스에서 CPU 사용량이 낮은 있을 수 있으므로 hello 동일한 시간 전반적인 시스템 CPU 커질 수 있습니다. CPU 사용량에서 제한 시간에 해당 하는 급증을 확인합니다.

#### <a name="resolution"></a>해결 방법
[배율](cache-how-to-scale.md) tooa 더 큰 캐시 CPU 용량이 더 큰 계층 또는 CPU 스파이크 원인을 확인 합니다. 

### <a name="server-side-bandwidth-exceeded"></a>서버 쪽 대역폭 초과
#### <a name="problem"></a>문제
크기가 다른 캐시 인스턴스는 어느 정도의 네트워크 대역폭을 사용할 수 있는지에 제한이 있습니다. Hello 서버 hello 사용 가능한 대역폭을 초과 하면 다음 데이터가 전송 되지 않습니다 toohello 클라이언트도 신속 하 게 합니다. Tootimeouts를 발생할 수 있습니다.

#### <a name="measurement"></a>측정
Hello를 모니터링할 수 있습니다 `Cache Read` hello hello 지정한 보고 간격 동안 메가바이트 (MB/s) 초당 hello 캐시에서 읽은 데이터 양의 메트릭을 합니다. 이 값이이 캐시에서 사용 되는 toohello 네트워크 대역폭을 해당 합니다. 서버 쪽 네트워크 대역폭 제한에 대 한 경고를 tooset를 원하는 경우이 사용 하 여 만들 수 있습니다 `Cache Read` 카운터입니다. 프로그램 판독값의 hello 값과 비교 [이 테이블](cache-faq.md#cache-performance) 다양 한 캐시 가격 책정 계층 및 크기에 대 한 대역폭 제한을 관찰 된 hello에 대 한 합니다.

#### <a name="resolution"></a>해결 방법
가격 책정 계층 및 캐시 크기에 대 한 최대 대역폭을 관찰 하는 hello 근처 일관 되 게 하려는 경우 고려해 야 [배율](cache-how-to-scale.md) tooa hello 값을 사용 하 여, 계층 또는 네트워크 대역폭 크기 가격 [가이테이블](cache-faq.md#cache-performance) 를 참조 합니다.

## <a name="stackexchangeredis-timeout-exceptions"></a>StackExchange.Redis 시간 제한 예외 조사
StackExchange.Redis는 기본값이 1000ms인 동기 작업에 대해 `synctimeout`이라는 이름의 구성 설정을 사용합니다. 에 로그인 하는 동기 호출을 완료 하지 다음 예제에서는 시간 초과 오류 유사한 toohello hello 규정 시간 hello StackExchange.Redis 클라이언트 throw 된 합니다.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


이 오류 메시지에는 hello 문제의 원인과 가능한 해결 toohello 안내 하는 데 도움이 되는 메트릭을 포함 되어 있습니다. hello 다음 표에서 오류 메시지 메트릭스 hello에 대 한 세부 정보.

| 오류 메시지 메트릭 | 세부 정보 |
| --- | --- |
| inst |Hello 마지막 시간 조각에서: 0 명령을 실행 한 |
| mgr |hello 소켓 관리자가 수행 `socket.select` 즉 요청 hello OS tooindicate 하는 소켓 toodo; 기본적으로: hello 판독기가 적극적으로 읽고 있지 hello 네트워크에서 작업이 생각 하지 때문에 toodo |
| 큐 |진행 중인 작업이 총 73건 있습니다. |
| qu |hello 진행 중인 작업의 6 hello 보내지 않은 큐에 있으며 toohello 아웃 바운드 네트워크가 아직 기록 되지 않은 |
| qs |그리고 진행 중인 작업의 67 toohello 서버 보낸 있지만 응답은 사용할 수 없습니다. hello 응답 수 `Not yet sent by hello server` 또는`sent by hello server but not yet processed by hello client.` |
| qc |0이 hello 진행 중인 작업의 회신에 알아보았습니다 않으며 표시 되지 않은 아직 인해 완료 상태로 hello 완료 루프에서 toowaiting |
| wr |현재 작성기는 (보내지 않은 6 요청 hello 의미는 무시 되지 않습니다) 바이트/activewriters |
| in |현재 판독기가 없습니다 및 0 바이트는 사용할 수 있는 toobe NIC 바이트/activereaders hello에 대 한 읽기 |

### <a name="steps-tooinvestigate"></a>단계 tooinvestigate
1. 가장 좋은 방법은 해야 패턴 tooconnect hello StackExchange.Redis 클라이언트를 사용할 때 다음 hello를 사용 하는 합니다.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    자세한 내용은 참조 [toohello 캐시 StackExchange.Redis를 사용 하 여 연결](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache)합니다.

1. Azure Redis Cache 및 hello 클라이언트 응용 프로그램 hello에 있는지 확인 하세요 Azure에서 동일한 지역입니다. 예를 들어 수 발생할 있습니다 시간 제한을 있을 경우 캐시 미국 동부 하지만 hello 클라이언트 West US에는 hello 요청 hello 내에 완료 하지 않는 `synctimeout` 간격 또는 있습니다 수 발생할 시간 제한을 로컬 개발 컴퓨터에서 디버깅 하는 경우. 
   
    toohave hello 캐시 좋습니다 하 고 hello 클라이언트에 동일 hello Azure 지역입니다. Hello를 설정 해야 지역 간 호출을 포함 하는 시나리오를 사용 하도록 설정한 경우 `synctimeout` 간격 tooa 값을 포함 하 여 hello 기본 1000 밀리초 간격 보다 크게는 `synctimeout` hello 연결 문자열의 속성입니다. hello 다음 예제와 StackExchange.Redis 캐시 연결 문자열 조각은 `synctimeout` 2000 밀리초입니다.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. 최신 버전의 hello hello를 사용 하 여 알아보기 위한 [StackExchange.Redis NuGet 패키지](https://www.nuget.org/packages/StackExchange.Redis/)합니다. 지속적으로 되 고 버그에 없는 고정 hello 코드 toomake 것 보다 강력한 tootimeouts hello 최신 버전이 하는 것이 중요 합니다.
3. 대역폭 제한 hello 서버 또는 클라이언트에 의해 바인딩된를 가져오는 요청이 있으면 오래 걸립니다을 toocomplete 있고이 인해 시간 초과 합니다. toosee에 시간 초과 되어 toonetwork 대역폭 hello 서버에서 발생 하는 경우 참조 [초과 하는 서버 쪽 대역폭](#server-side-bandwidth-exceeded)합니다. 프로그램 timeout이 tooclient 네트워크 대역폭 인해 toosee 참조 [초과 하는 클라이언트 쪽 대역폭](#client-side-bandwidth-exceeded)합니다.
4. Hello 서버 또는 클라이언트 hello에 바인딩된 CPU를 시작 하면?
   
   * 하면 hello 요청 toonot 될 수 있는 클라이언트에서 CPU에 의해 바인딩된 시작 되었는지 확인 하 고 hello 내에서 처리 되지 `synctimeout` 시간 초과 오류를 발생 시킬 간격입니다. 클라이언트 크기를 더 큰 tooa 이동 하거나 hello 부하를 분산 유용 toocontrol이 합니다. 
   * Hello를 모니터링 하 여 hello 서버에 있는지 확인 합니다. CPU를 가져오는 바인딩된 `CPU` [성능 메트릭 캐시](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)합니다. Redis는 CPU 바운드도 지정 하면 해당 하는 동안 발생 하는 요청 tootimeout를 요청 합니다. tooaddress hello를 배포할 수 있습니다이 프리미엄 캐시의 여러 분할 영역 간에 부하를 또는 tooa 더 큰 크기 또는 가격 책정 계층을 업그레이드 합니다. 자세한 내용은 [서버 쪽 대역폭 초과](#server-side-bandwidth-exceeded)를 참조합니다.
5. 시간이 오래 tooprocess hello 서버에서 수행 하는 명령을 있습니까? 장기 실행 시간이 오래 tooprocess hello redis 서버에서 수행 하는 명령을 시간 초과가 발생할 수 있습니다. 장기 실행 명령의 몇 가지 예로 다수의 키 작동을 요하는 `mget`, `keys *` 또는 형편없게 짜여진 lua 스크립트 등이 있습니다. Hello를 사용 하거나 hello cli redis 클라이언트를 사용 하 여 tooyour Azure Redis Cache 인스턴스에 연결할 수 [Redis 콘솔](cache-configure.md#redis-console) 및 실행된 hello [SlowLog](http://redis.io/commands/slowlog) 명령 toosee 요청이 예상 보다 오래 걸립니다. Redis 서버와 StackExchange.Redis는 작은 수의 큰 요청보다 많은 수의 작은 요청을 위해 최적화되어 있습니다. 데이터를 더 작은 청크로 분할한다면 다음을 향상시킵니다. 
   
    Redis cli 및 stunnel를 사용 하 여 toohello Azure Redis 캐시 SSL 끝점 연결 방법에 대 한 자세한 내용은 참조 hello [미리 보기 릴리스 Redis 용 ASP.NET 세션 상태 공급자 발표](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) 블로그 게시물입니다. 자세한 내용은 [SlowLog](http://redis.io/commands/slowlog)를 참조하세요.
6. 높은 Redis 서버 부하로 시간 초과가 발생할 수 있습니다. Hello를 모니터링 하 여 hello 서버 부하를 모니터링할 수 있습니다 `Redis Server Load` [성능 메트릭 캐시](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)합니다. 100 (최대 값)의 서버 부하를 해당 hello redis 서버 하 고 있었습니다, 유휴 시간이 없다면 요청 처리 의미 합니다. 특정 요청을 모든 hello 서버 기능을 수행 하는 경우에서 toosee는 hello 이전 단락에 설명 된 대로 hello SlowLog 명령을 실행 합니다. 자세한 내용은 [높은 CPU 사용량/서버 로드](#high-cpu-usage-server-load)를 참조하세요.
7. 네트워크 문제가 발생할 수 있습니다 hello 클라이언트 쪽에서 다른 이벤트 있었습니까? 위로 또는 아래로 hello 클라이언트 인스턴스 수를 크기 조정 또는 새 버전의 hello 클라이언트 배포와 같은 이벤트 했습니다 (웹, 작업자 역할 또는 Iaas VM) hello 클라이언트 확인 또는 자동 크기 조정 사용? 자동 크기 조정 또는 위쪽/아래쪽 크기 조정 될 수 있다는 알게 되었지만 테스트를 몇 초 동안 아웃 바운드 네트워크 연결 손실 될 수 있습니다. StackExchange.Redis 코드 탄력적 toosuch 이벤트를 다시 연결 됩니다. 재연결의이 시간 동안 hello 큐의 모든 요청 시간 초과 될 수 있습니다.
8. 앞에 여러 개의 작은 요청 toohello 시간이 초과 되었습니다 Redis 캐시 큰 요청 있었습니까? 매개 변수를 hello `qs` hello 오류 메시지 알려 요청의 개수 hello 클라이언트 toohello 서버에서 보냈지만 응답을 아직 처리 하지 않은 합니다. StackExchange.Redis는 하나의 TCP 연결을 사용하고 한 번에 하나의 응답만 읽을 수 있기 때문에 이 값은 계속 증가할 수 있습니다. Hello 첫 번째 작업 제한 시간이 초과 하는 경우에 hello 데이터 hello 서버에서 전송 되는 중지 되지 않습니다 및 다른 요청은 완료 되 면 시간 초과 발생 될 때까지 차단 됩니다. 한 가지 해결 확률이 toominimize hello 시간 제한 값이 크면 더 작은 청크로 분할 하 고 캐시 작업에 충분히 큰지 확인 하 여. 다른 가능한 방법은 toouse의 풀 `ConnectionMultiplexer` 클라이언트에 개체를 로드 이상 hello 선택 `ConnectionMultiplexer` 새 요청을 보낼 때. 다른 요청 tooalso 제한 시간 때문 하나의 제한을 막아야 합니다.
9. 사용 중인 경우 `RedisSessionStateprovider`, hello 다시 시도 제한 시간을 올바르게 설정 했는지 확인 합니다. `retrytimeoutInMilliseconds`는 `operationTimeoutinMilliseonds`보다 높아야 합니다. 그렇지 않으면 재시도가 발생하지 않습니다. 다음 예제는 hello에 `retrytimeoutInMilliseconds` too3000 설정 됩니다. 자세한 내용은 참조 [Azure Redis Cache 용 ASP.NET 세션 상태 공급자](cache-aspnet-session-state-provider.md) 및 [toouse 세션 상태 공급자와 출력 캐시 공급자의 구성 매개 변수를 hello 어떻게](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration)합니다.

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. 하 여 hello Azure Redis 캐시 서버에서 메모리 사용량 확인 [모니터링](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` 및 `Used Memory`합니다. 제거 정책 이면 Redis가 시작 될 때 키를 제거 하는 방식 `Used_Memory` 도달 hello 캐시 크기. 이상적으로 `Used Memory RSS`는 `Used memory`보다 약간만 높아야 합니다. 큰 차이는 메모리 조각화 (내부 또는 외부)가 심함을 의미합니다. 때 `Used Memory RSS` 는 보다 작은 `Used Memory`, hello 캐시 메모리의 일부 hello 운영 체제에 의해 교체 된 것을 의미 합니다. 이 경우 일부 상당한 대기 시간을 예상할 수 있습니다. Redis에 없기 때문에 컨트롤을 통해 높은 toomemory 페이지 매핑된 해당 할당은 어떻게 `Used Memory RSS` 메모리 사용량에 스파이크가의 hello 결과 경우가 많습니다. Redis 메모리를 해제 하면 hello 메모리 다시 toohello 할당자에 제공 됩니다 및 hello 할당자 되거나 hello 메모리 백 toohello 시스템을 제공 하지 못할 수도 있습니다. Hello 간에 차이가 있을 수 있습니다 `Used Memory` hello 운영 체제에서 보고 값 및 메모리 사용 합니다. 때문일 수 있습니다 toohello 팩트 메모리 사용 되었으며에 발표 Redis에서 뒤로 toohello 시스템 제공 되지 않습니다. toohelp은 hello 다음 단계를 수행할 수 있습니다 하는 메모리 문제를 완화 합니다.
   
   * Hello 시스템에서 메모리를 제한 사항과 실행 되지 않는 되도록 hello 캐시 tooa 더 큰 크기를 업그레이드 하십시오.
   * 오래 된 값 사전 제거 되는 있도록 hello 키 만료 시간을 설정 합니다.
   * 모니터 hello hello `used_memory_rss` 메트릭을 캐시 합니다. 이 값이 해당 캐시의 hello 크기에 가까워지면 가능성이 toostart 성능 문제가 표시 됩니다. 캐시 크기를 더 큰 tooa 업그레이드 또는 프리미엄 캐시를 사용 하는 경우 여러 분할 영역 간에 hello 데이터를 배포 합니다.
   
   자세한 내용은 참조 [hello 서버에서 메모리가 중](#memory-pressure-on-the-server)합니다.

## <a name="additional-information"></a>추가 정보
* [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [어떻게 하나요 벤치 마크 하 고 테스트할 수 내 캐시의 성능을 hello?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [어떻게 Redis 명령을 실행할 수 있나요?](cache-faq.md#how-can-i-run-redis-commands)
* [Azure Redis 캐시 하는 toomonitor 방법](cache-how-to-monitor.md)


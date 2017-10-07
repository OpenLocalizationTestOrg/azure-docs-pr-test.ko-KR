---
title: "Redis 캐시 FAQ aaaAzure | Microsoft Docs"
description: "Hello Azure Redis Cache에 대 한 toocommon 질문, 패턴 및 모범 사례를 응답에 대해 알아봅니다"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Azure Redis Cache FAQ
Hello Azure Redis Cache에 대 한 toocommon 질문, 패턴 및 모범 사례를 응답에 대해 알아봅니다.

## <a name="what-if-my-question-isnt-answered-here"></a>여기서 내 질문에 대답하지 않으면 어떻게 하나요?
질문하려는 내용이 아래 목록에 나와 있지 않으면 알려 주세요. 대답을 확인하는 방법을 알려 드리겠습니다.

* 이 FAQ의 hello 끝에 hello 메모에 질문을 게시할 수 있으며 hello Azure 캐시 팀 및 다른 커뮤니티 구성원 들이 문서에 대 한 의견을 교환 수 있습니다.
* 더 광범위 한 tooreach hello에 질문을 게시할 수 있습니다 [Azure 캐시 MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) hello Azure 캐시 팀과 hello 커뮤니티의 다른 구성원에 문의 하 고 있습니다.
* 원하는 toomake 기능 요청을 제출할 수 있습니다 요청 및 아이디어 너무[Azure Redis 캐시 사용자 음성](https://feedback.azure.com/forums/169382-cache)합니다.
* 보낼 수도 있습니다는 전자 메일에서 toous [Azure 캐시 외부 피드백](mailto:azurecache@microsoft.com)합니다.

## <a name="azure-redis-cache-basics"></a>Azure Redis Cache 기본 사항
이 섹션의 Faq hello Azure Redis Cache의 hello 기본 사항 중 일부를 다룬 합니다.

* [Azure Redis Cache란?](#what-is-azure-redis-cache)
* [Azure Redis Cache를 시작하려면 어떻게 하나요?](#how-can-i-get-started-with-azure-redis-cache)

다음 Faq 기본 개념 및 Azure Redis Cache에 대 한 질문을 포함 하 고 중 하나에 대 한 답변은 hello hello 다른 FAQ 섹션.

* [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](#what-redis-cache-offering-and-size-should-i-use)
* [어떤 Redis Cache 클라이언트를 사용할 수 있나요?](#what-redis-cache-clients-can-i-use)
* [Azure Redis Cache에 대한 로컬 에뮬레이터가 있나요?](#is-there-a-local-emulator-for-azure-redis-cache)
* [내 캐시의 hello 상태와 성능을 모니터링 하려면 어떻게 해야 합니까?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>계획 FAQ
* [어떤 Redis Cache 제품 및 크기를 사용해야 하나요?](#what-redis-cache-offering-and-size-should-i-use)
* [Azure Redis Cache 성능](#azure-redis-cache-performance)
* [어떤 영역에 내 캐시를 배치해야 하나요?](#in-what-region-should-i-locate-my-cache)
* [Azure Redis Cache에 대한 요금은 어떻게 청구되나요?](#how-am-i-billed-for-azure-redis-cache)
* [Azure Government 클라우드, Azure 중국 클라우드 또는 Microsoft Azure Germany에서 Azure Redis Cache를 사용할 수 있나요?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>개발 FAQ
* [Hello StackExchange.Redis 구성 옵션의 기능은 무엇입니까?](#what-do-the-stackexchangeredis-configuration-options-do)
* [어떤 Redis Cache 클라이언트를 사용할 수 있나요?](#what-redis-cache-clients-can-i-use)
* [Azure Redis Cache에 대한 로컬 에뮬레이터가 있나요?](#is-there-a-local-emulator-for-azure-redis-cache)
* [어떻게 Redis 명령을 실행할 수 있나요?](#how-can-i-run-redis-commands)
* [Azure Redis Cache는 MSDN 클래스 라이브러리 참조 중 일부와 같은 다른 Azure 서비스 hello 있는 하지 않는 이유는 무엇입니까?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Azure Redis Cache를 PHP 세션 캐시로 사용할 수 있나요?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Redis 데이터베이스란?](#what-are-redis-databases)

## <a name="security-faqs"></a>보안 FAQ
* [TooRedis 연결 하기 위한 hello 비 SSL 포트를 사용 해야는 경우](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>프로덕션 FAQ
* [프로덕션 모범 사례에는 어떤 것이 있나요?](#what-are-some-production-best-practices)
* [무엇 인가요 일반적인 Redis 명령을 사용 하는 경우 몇 가지 고려 사항 hello?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [어떻게 하나요 벤치 마크 하 고 테스트할 수 내 캐시의 성능을 hello?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [ThreadPool 증가에 대한 중요한 세부 정보](#important-details-about-threadpool-growth)
* [StackExchange.Redis를 사용 하는 경우 서버 GC tooget hello 클라이언트에서 더 많은 처리량을 사용](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [성능 고려 사항 및 연결](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>모니터링 및 문제 해결 FAQ
hello Faq의이 섹션 커버 일반 모니터링 및 문제 해결 질문 합니다. 모니터링 및 Azure Redis Cache 인스턴스 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [어떻게 toomonitor Azure Redis 캐시](cache-how-to-monitor.md) 및 [어떻게 tootroubleshoot Azure Redis 캐시](cache-how-to-troubleshoot.md)합니다.

* [내 캐시의 hello 상태와 성능을 모니터링 하려면 어떻게 해야 합니까?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [왜 시간 초과가 표시되나요?](#why-am-i-seeing-timeouts)
* [클라이언트는 hello 캐시에서 연결이 끊어진 이유는?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>이전 캐시 제공 FAQ
* [내게 적합한 Azure 캐시 기능](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Azure Redis Cache란?
Azure Redis 캐시 hello 인기 있는 오픈 소스 기반 [Redis cache](http://redis.io)합니다. 제공 tooa 안전한 전용된 Redis 캐시, microsoft에서 관리 및 액세스 Azure 내에서 모든 응용 프로그램에서 액세스 합니다. 자세한 개요에 대 한 참조 hello [Azure Redis Cache](https://azure.microsoft.com/services/cache/) azure.com 제품 페이지.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Azure Redis Cache를 시작하려면 어떻게 하나요?
몇 가지 방법으로 Azure Redis Cache를 시작할 수 있습니다.

* [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) 및 [Python](cache-python-get-started.md)에 대해 사용할 수 있는 자습서 중 하나를 확인해볼 수 있습니다.
* 확인할 수 있습니다 [어떻게 tooBuild 고성능 앱 사용 하 여 Microsoft Azure Redis Cache](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/)합니다.
* Toouse Redis 어떻게 하 여 프로젝트 toosee의 hello 개발 언어와 일치 하는 hello 클라이언트에 대 한 hello 클라이언트 설명서 아웃 확인할 수 있습니다. Azure Redis Cache를 사용할 수 있는 많은 Redis 클라이언트가 있습니다. Redis 클라이언트 목록에 대해서는 [http://redis.io/clients](http://redis.io/clients)를 참조하세요.

Azure 계정이 없는 경우 다음을 수행할 수 있습니다.

* [Azure 계정을 무료로 개설할 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Azure 서비스를 유료 아웃 사용된 tootry 일 수 있는 크레딧을 얻게. Hello 크레딧을 모두 사용 된 후에 hello 계정을 유지 하 고 무료 Azure 서비스 및 기능을 사용할 수 있습니다.
* [Visual Studio 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero) MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>어떤 Redis Cache 제품 및 크기를 사용해야 하나요?
각 Azure Redis Cache 제품은 서로 다른 수준의 **크기**, **대역폭**, **고가용성** 및 **SLA** 옵션을 제공합니다.

캐시 제공 량 선택에 대 한 고려 사항은 hello 다음과가 같습니다.

* **메모리**: hello 기본 계층과 표준 계층 250MB-53 GB를 제공 합니다. hello Premium 계층 too530 GB를 제공합니다. 자세한 내용은 [Azure Redis Cache 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요.
* **네트워크 성능을**: hello 프리미엄 계층은 더 많은 대역폭 비교 tooStandard 또는 Basic 높은 처리량을 필요로 하는 작업 부하를 설정한 경우. 또한 각 계층 내의 대형 크기 캐시 있으며, 더 많은 대역폭 hello 캐시를 호스팅하는 VM 내부 hello 때문에 Hello 참조 [테이블 다음](#cache-performance) 자세한 정보에 대 한 합니다.
* **처리량**: hello Premium 계층 hello 최대 사용 가능한 처리량을 제공 합니다. Hello 캐시 서버 또는 클라이언트 hello 대역폭 한계에 도달 하면 hello 클라이언트 쪽의 시간 제한이 발생할 수 있습니다. 자세한 내용은 다음 표는 hello를 참조 하세요.
* **높은 가용성/SLA**: Azure Redis Cache 표준/프리미엄 캐시를 사용할 수 있는지 이상 hello 시간의 99.9% 보장 합니다. toolearn SLA는에 대 한 자세한 참조 [Azure Redis Cache 가격](https://azure.microsoft.com/support/legal/sla/cache/v1_0/)합니다. SLA hello에서는 연결 toohello 캐시 끝점에 대해서만 설명 합니다. hello SLA 데이터 손실 로부터 보호를 다루지 않습니다. 데이터 손실 방지 hello 프리미엄 계층 tooincrease 탄력성에서 hello Redis 데이터 지 속성 기능을 사용 하는 것이 좋습니다.
* **Redis 데이터 지 속성**: hello 프리미엄 계층에서 허용 하면 toopersist hello 캐시 데이터는 Azure 저장소 계정에 있습니다. 기본/표준 캐시에서 모든 hello 데이터가 메모리에만 저장 됩니다. 기본 인프라 문제가 있는 경우 잠재적인 데이터 손실이 있을 수 있습니다. 데이터 손실 방지 hello 프리미엄 계층 tooincrease 탄력성에서 hello Redis 데이터 지 속성 기능을 사용 하는 것이 좋습니다. Azure Redis Cache는 Redis 지속성에서 RDB 및 AOF(출시 예정) 옵션을 제공합니다. 자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 지 속성 tooconfigure](cache-how-to-premium-persistence.md)합니다.
* **Redis 클러스터**: 여러 Redis 노드에서 toocreate tooshard 데이터 또는 53 GB 보다 큰 캐시를 사용할 수 있습니다 Redis 클러스터링 hello 프리미엄 계층에서 사용할 수 있습니다. 각 노드는 고가용성을 위해 주/복제본 캐시 쌍으로 구성됩니다. 자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](cache-how-to-premium-clustering.md)합니다.
* **보안 및 네트워크 격리 강화**: Azure 가상 네트워크 (VNET) 배포에서는 강화 된 보안 및 액세스 제어 정책 서브넷 뿐 Azure Redis Cache에 대 한 격리 및 기타 기능 toofurther 액세스를 제한 합니다. 자세한 내용은 참조 [Premium Azure Redis Cache에 대 한 tooconfigure 가상 네트워크를 지 원하는 방법](cache-how-to-premium-vnet.md)합니다.
* **Redis 구성**: hello 표준 및 프리미엄 계층에서는 키 스페이스 알림에서에 Redis를 구성할 수 있습니다.
* **최대 클라이언트 연결**: hello 프리미엄 계층은 hello tooRedis, 더 큰 크기의 캐시에 대 한 연결 수가 높을수록와 연결할 수 있는 클라이언트의 최대 수를 제공 합니다. 자세한 내용은 [Azure Redis Cache 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요.
* **Redis 서버에 대 한 핵심 전용**: hello 프리미엄 계층에서는 모든 캐시 크기는 전용된 코어 Redis에 대 한 합니다. Hello 기본/표준 계층에서 C1 크기 hello 있고 위에 Redis 서버에 대 한 전용된 코어.
* **Redis는 단일 스레드** 이므로 3개 이상의 코어를 사용해도 2개 코어만 사용하는 경우에 비해 추가적인 이점이 없지만 VM 크기가 더 크면 일반적으로 작은 크기보다 대역폭이 더 큽니다. Hello 캐시 서버 또는 클라이언트 hello 대역폭 한계에 도달 하면 hello 클라이언트 쪽에서 시간 제한을 수신 있습니다.
* **성능 향상**: hello Premium 계층에 캐시가 있는 빠른 프로세서에서 하드웨어에 배포 되 더 나은 성능을 비교 toohello 기본 또는 표준 계층을 제공 합니다. 프리미엄 계층 캐시는 처리량은 더 높고 대기 시간은 더 짧습니다.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Azure Redis Cache 성능
hello 다음 표에서 표준의 다양 한 크기를 테스트 하는 동안 관찰 된 hello 최대 대역폭 값 및 프리미엄 캐시를 사용 하 여 `redis-benchmark.exe` hello Azure Redis 캐시 끝점에 대해 Iaas VM에서. 

>[!NOTE] 
>이러한 값은 보장되지 않으며 해당 수치에 대한 SLA는 없지만 일반적인 수치입니다. 로드 해야 응용 프로그램에 대 한 사용자 고유의 응용 프로그램 toodetermine hello 알맞은 캐시 크기를 테스트 합니다.
>
>

이 테이블에서 hello 다음 결론을 내릴 수 있습니다.

* Hello 캐시의 상위 수준에 같은 크기는 hello에 대 한 처리량 비교 toohello 표준 계층으로 Premium 계층을 hello 합니다. 예를 들어 6 GB 캐시와 처리량 p 1의은 180, 000 RPS 비교 too49, c 3에 대 한 000으로입니다.
* Redis 클러스터링와 함께 hello 클러스터의 분할 영역 (노드) hello 수를 늘리면 처리량 선형으로 증가 합니다. 예를 들어 10 개의 분할 된 데이터베이스의 P4 클러스터를 만드는 경우 다음 hello 사용할 수 있는 처리량은 400000 * RPS 10 = 4 백만 합니다.
* 더 큰 키 크기에 대 한 처리량은 비교 toohello 표준 계층으로 hello Premium 계층에 더 합니다.

| 가격 책정 계층  | 크기 | CPU 코어 | 사용 가능한 대역폭 | 1KB 값 크기 |
| --- | --- | --- | --- | --- |
| **표준 캐시 크기** | | |**Mb/s(초당 메가비트) / MB/s(초당 메가바이트)** |**초당 요청 수(RPS)** |
| C0 |250MB |공유됨 |5/0.625 |600 |
| C1 |1 GB |1 |100/12.5 |12,200 |
| C2 |2.5GB |2 |200/25 |24,000 |
| C3 |6GB |4 |400/50 |49,000 |
| C4 |13GB |2 |500/62.5 |61,000 |
| C5 |26GB |4 |1,000 / 125 |115,000 |
| C6 |53GB |8 |2,000 / 250 |150,000 |
| **프리미엄 캐시 크기** | |**분할 영역당 CPU 코어** | **Mb/s(초당 메가비트) / MB/s(초당 메가바이트)** |**초당 요청 수(RPS), 분할된 데이터베이스당** |
| P1 |6GB |2 |1,500 / 187.5 |180,000 |
| P2 |13GB |4 |3,000 / 375 |360,000 |
| P3 |26GB |4 |3,000 / 375 |360,000 |
| P4 |53GB |8 |6,000 / 750 |400,000 |

Hello 다운로드 방법은 같은 도구를 Redis에 대 한 `redis-benchmark.exe`, hello 참조 [Redis 명령을 실행 하는 방법?](#cache-commands) 섹션.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>어떤 영역에 내 캐시를 배치해야 하나요?
최상의 성능 및 낮은 대기 시간에 대 한 Azure Redis Cache hello에서 찾을 캐시 클라이언트 응용 프로그램과 같은 지역입니다.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Azure Redis Cache에 대한 요금은 어떻게 청구되나요?
Azure Redis Cache 가격 책정에 대해서는 [여기](https://azure.microsoft.com/pricing/details/cache/)를 참조하세요. 가격 책정 페이지 hello로 시간당 가격을 나열 합니다. 캐시에는 캐시를 삭제 하는 hello 시간까지 hello 캐시는 생성 하는 hello 시간에서 분 단위로 청구 됩니다. 또는 캐시의 hello 청구 일시 중지에 대 한 옵션이 있습니다.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Azure Government 클라우드, Azure 중국 클라우드 또는 Microsoft Azure Germany에서 Azure Redis Cache를 사용할 수 있나요?
예, Azure Government 클라우드, Azure 중국 클라우드 및 Microsoft Azure Germany에서 Azure Redis Cache를 사용할 수 있습니다. hello Url에 액세스 하 고 Azure Redis 캐시를 관리 하기 위한 Azure 공용 클라우드와 비교 하는 이러한 클라우드에서 서로 다릅니다. 

| 클라우드   | Redis에 대한 Dns 접미사            |
|---------|---------------------------------|
| 공용  | *.redis.cache.windows.net       |
| 미국 정부  | *.redis.cache.usgovcloudapi.net |
| 독일 | *.redis.cache.cloudapi.de       |
| 중국   | *.redis.cache.chinacloudapi.cn  |

다른 클라우드와 함께 Azure Redis Cache를 사용 하는 경우 고려 사항에 대 한 자세한 내용은 링크를 따라 hello를 참조 하세요.

- [Azure Government 데이터베이스 - Azure Redis Cache](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure 중국 클라우드 - Azure Redis Cache](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)

Azure Government 클라우드, Azure 중국 클라우드 및 Microsoft Azure 독일에는 PowerShell과 함께 Azure Redis Cache를 사용 하는 방법은 참조 하십시오. [어떻게 tooconnect tooother 클라우드-Azure Redis 캐시 PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds)합니다.

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Hello StackExchange.Redis 구성 옵션의 기능은 무엇입니까?
StackExchange.Redis에는 많은 옵션이 있습니다. 이 섹션 hello 일반 설정 중 일부에 대해 설명 합니다. StackExchange.Redis 옵션에 대한 자세한 내용은 [StackExchange.Redis 구성](https://stackexchange.github.io/StackExchange.Redis/Configuration)을 참조하세요.

| ConfigurationOptions | 설명 | 권장 사항 |
| --- | --- | --- |
| AbortOnConnectFail |Tootrue, 설정 된 경우 hello 연결에서 네트워크 오류가 발생 한 후 다시 연결 되지 않습니다. |자동으로 다시 연결 StackExchange.Redis를 toofalse 설정 됩니다. |
| ConnectRetry |hello toorepeat 연결 시도 횟수는 동안 초기 연결 합니다. |Hello 다음 지침에 대 한 메모를 참조 하십시오. |
| ConnectTimeout |연결 작업의 시간 제한(ms)입니다. |Hello 다음 지침에 대 한 메모를 참조 하십시오. |

일반적으로 클라이언트 hello의 hello 기본값이 면 충분 합니다. 작업에 따라 hello 옵션을 미세 조정할 수 있습니다.

* **재시도**
  * ConnectRetry 및 ConnectTimeout hello 일반적인 지침 toofail 빠른 이며 다시 시도 하십시오. 이 지침은 작업 및 얼마나 많은 시간을 사용 하면 클라이언트 tooissue Redis 명령에 대 한 평균을 내 고 응답을 받을 기반으로 합니다.
  * 연결 상태를 확인하고 직접 다시 연결하는 대신 StackExchange.Redis가 자동으로 다시 연결하도록 합니다. **Hello ConnectionMultiplexer.IsConnected 속성을 사용 하지 않도록**합니다.
  * -Snowballing 경우가 발생할 수 있습니다는 문제를 다시 시도 중인지 및 hello 스노우 볼 다시 시도 하 고 복구 되지 않습니다. 에 설명 된 대로 지 수 백오프 다시 시도 알고리즘을 사용 하 여 고려해 야 snowballing 발생 하는 경우 [일반적인 지침을 다시 시도](../best-practices-retry-general.md) hello Microsoft 패턴 및 규칙 그룹에 의해 게시 합니다.
* **시간 제한 값**
  * 사용자 작업을 고려해 야 하 고 hello 값을 적절 하 게 설정 합니다. 큰 값을 저장 하는 경우 hello 시간 제한 tooa 더 높은 값을 설정 합니다.
  * 설정 `AbortOnConnectFail` toofalse StackExchange.Redis를 다시 연결 하도록 합니다.
  * Hello 응용 프로그램에 대 한 단일 ConnectionMultiplexer 인스턴스를 사용 합니다. 에 표시 된 대로 LazyConnection toocreate 연결 속성에 의해 반환 되는 단일 인스턴스를 사용할 수 있습니다 [hello ConnectionMultiplexer 클래스를 사용 하 여 toohello 캐시 연결](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache)합니다.
  * 집합 hello `ConnectionMultiplexer.ClientName` 속성 tooan 응용 프로그램 인스턴스 고유 이름 진단 목적입니다.
  * 사용자 지정 작업에 여러 개의 `ConnectionMultiplexer` 인스턴스를 사용합니다.
      * 응용 프로그램에 다양한 부하가 있는 경우 이 모델을 따를 수 있습니다. 예:
      * 큰 키를 처리하기 위한 멀티플렉서 1개가 있습니다.
      * 작은 키를 처리하기 위한 멀티플렉서 1개가 있습니다.
      * 사용하는 각 ConnectionMultiplexer의 연결 시간 제한 및 다시 시도 논리에 대해 다른 값을 설정할 수 있습니다.
      * 집합 hello `ClientName` 각 멀티플렉서 toohelp 진단을는 속성입니다.
      * 이 지침은 당 toomore 간소화 된 대기 시간을 야기할 수 `ConnectionMultiplexer`합니다.

### <a name="what-redis-cache-clients-can-i-use"></a>어떤 Redis Cache 클라이언트를 사용할 수 있나요?
Redis에 대 한 hello 뛰어난 기능 중 하나는 많은 다양 한 개발 언어를 지 원하는 클라이언트 수는 있습니다. 클라이언트의 현재 목록에 대해서는 [Redis 클라이언트](http://redis.io/clients)를 참조하세요. 여러 가지 서로 다른 언어 및 클라이언트를 포함 하는 자습서를 참조 하십시오. [어떻게 toouse Azure Redis 캐시](cache-dotnet-how-to-use-azure-redis-cache.md) hello 언어 전환기 hello 문서의 hello 위쪽에서 hello 원하는 언어를 클릭 합니다.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Azure Redis Cache에 대한 로컬 에뮬레이터가 있나요?
Azure Redis Cache에 대 한 로컬 에뮬레이터 없는 이지만 hello에서 redis server.exe의 hello MSOpenTech 버전을 실행할 수 있습니다 [명령줄 도구를 Redis](https://github.com/MSOpenTech/redis/releases/) 에 로컬 컴퓨터 및 연결 tooit tooget 비슷한 경험 tooa 로컬 캐시 다음 예제는 hello에 나와 있는 것 처럼 에뮬레이터:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


선택적으로 구성할 수는 [redis.conf](http://redis.io/topics/config) 파일 toomore hello 일치 [기본 캐시 설정](cache-configure.md#default-redis-server-configuration) 온라인 Azure Redis 캐시에 원하는 경우.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>어떻게 Redis 명령을 실행할 수 있나요?
에 나열 된 hello 명령 중 하나를 사용할 수 [Redis 명령](http://redis.io/commands#) 에 나열 된 hello 명령을 제외한 [Azure Redis Cache에서 지원 되지 않는 명령 Redis](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache)합니다. 옵션 toorun Redis 명령을 사용할 수 있습니다.

* 표준 또는 프리미엄 캐시를 사용 하도록 설정한 경우 hello를 사용 하 여 Redis 명령을 실행할 수 있습니다 [Redis 콘솔](cache-configure.md#redis-console)합니다. hello Redis 콘솔 hello Azure 포털에서에서 Redis 명령을 안전 하 게 toorun를 제공합니다.
* Hello Redis 명령줄 도구를 사용할 수 있습니다. 수행 toouse, 다음 단계 hello:
* Hello 다운로드 [명령줄 도구를 Redis](https://github.com/MSOpenTech/redis/releases/)합니다.
* Toohello 캐시를 사용 하 여 연결 `redis-cli.exe`합니다. Hello-h 스위치 및 사용 하 여-a hello 다음 예제와 같이 hello 키를 사용 하 여 hello 캐시 끝점에 전달 합니다.
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> hello Redis 명령줄 도구에서 작동 하지 않는 hello SSL 포트와 같은 유틸리티를 사용할 수 있지만 `stunnel` toosecurely hello의 hello 지침에 따라 hello 도구 toohello SSL 포트에 연결 [용 ASP.NET 세션 상태 공급자 발표 미리 보기 릴리스 redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) 블로그 게시물입니다.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Azure Redis Cache는 MSDN 클래스 라이브러리 참조 중 일부와 같은 다른 Azure 서비스 hello 있는 하지 않는 이유는 무엇입니까?
Microsoft Azure Redis Cache는 hello 인기 있는 오픈 소스 Redis Cache에 근거 하며 광범위 한에서 액세스할 수 [Redis 클라이언트](http://redis.io/clients) 많은 프로그래밍 언어에 대 한 합니다. 각 클라이언트에는 toohello Redis 캐시 인스턴스를 사용 하 여 호출 하는 자체 API [Redis 명령](http://redis.io/commands)합니다.

클라이언트마다 다르기 때문에 MSDN에 하나의 중앙 집중식 클래스 참조는 없고, 각 클라이언트가 자체 참조 설명서를 유지 관리합니다. 또한 toohello 참조 설명서, 다른 언어와 캐시 클라이언트를 사용 하 여 Azure Redis 캐시 tooget 시작 하는 방법을 보여 주는 몇 가지 자습서. tooaccess 이러한 자습서를 참조 [어떻게 toouse Azure Redis 캐시](cache-dotnet-how-to-use-azure-redis-cache.md) hello 언어 전환기 hello 문서의 hello 위쪽에서 hello 원하는 언어를 클릭 합니다.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Azure Redis Cache를 PHP 세션 캐시로 사용할 수 있나요?
Azure Redis Cache는 PHP 세션 캐시 toouse hello 연결 문자열 tooyour Azure Redis 캐시 인스턴스를 지정 하는 예, `session.save_path`합니다.

> [!IMPORTANT]
> URL 해야 Azure Redis Cache는 PHP 세션 캐시를 사용할 때는 hello 다음 예제와 같이 hello 보안 키 사용 되는 tooconnect toohello 캐시를 인코딩합니다.
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Hello 키 URL로 인코딩된 경우와 같은 메시지와 함께 예외가 나타날 수 있습니다.`Failed tooparse session.save_path`
>
>

Redis Cache를 사용 하 여 hello PhpRedis 클라이언트와 함께 하는 PHP 세션 캐시에 대 한 자세한 내용은 참조 [PHP 세션 처리기](https://github.com/phpredis/phpredis#php-session-handler)합니다.

### <a name="what-are-redis-databases"></a>Redis 데이터베이스란?

Redis 데이터베이스는 hello 내에서 데이터의 논리적 분리만 Redis 동일 합니다. hello 캐시 메모리 모든 hello 데이터베이스 간에 공유 되 고 hello 키/값이 해당 데이터베이스에 저장 된에 지정된 된 데이터베이스의 실제 메모리 사용량에 따라 달라 집니다. 예를 들어 C6 캐시에는 53GB의 메모리가 있습니다. 하나의 데이터베이스에 모든 53GB tooput를 선택할 수도 있고 여러 데이터베이스 간에 분할할 수 있습니다. 

> [!NOTE]
> 클러스터링을 활성화하여 프리미엄 Azure Redis Cache를 사용하는 경우 데이터베이스 0만 사용할 수 있습니다. 이 제한은 경우 내장 Redis 제한이 이며 특정 tooAzure Redis Cache 않습니다. 자세한 내용은 참조 [필요 합니까 toomake 클러스터링 모든 변경 내용을 toomy 클라이언트 응용 프로그램 toouse?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>TooRedis 연결 하기 위한 hello 비 SSL 포트를 사용 해야는 경우
Redis 서버는 기본적으로 SSL을 지원하지 않지만 Azure Redis Cache는 지원합니다. 클라이언트가 원하는 StackExchange.Redis, 같은 SSL tooAzure Redis Cache를 연결 하는 경우 SSL을 사용 해야 합니다.

>[!NOTE]
>hello 비 SSL 포트는 새 Azure Redis 캐시 인스턴스에 대 한 기본적으로 비활성화 됩니다. 클라이언트 SSL을 지원 하지 않으면 hello의 hello 지침에 따라 hello 비 SSL 포트를 설정 해야 하는 경우 [액세스 포트](cache-configure.md#access-ports) hello 섹션 [Azure Redis Cache에서 캐시 구성](cache-configure.md) 문서.
>
>

와 같은 도구를 redis `redis-cli` hello SSL 포트를 사용 하지 않는 같은 유틸리티를 사용할 수 있지만 `stunnel` toosecurely hello의 hello 지침에 따라 hello 도구 toohello SSL 포트에 연결 [ASP.NET 세션 상태 공급자 발표 미리 보기 릴리스에서 Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) 블로그 게시물입니다.

Hello 다운로드 방법은 Redis 도구, 참조 hello [Redis 명령을 실행 하는 방법?](#cache-commands) 섹션.

### <a name="what-are-some-production-best-practices"></a>프로덕션 모범 사례에는 어떤 것이 있나요?
* [StackExchange.Redis 모범 사례](#stackexchangeredis-best-practices)
* [구성 및 개념](#configuration-and-concepts)
* [성능 테스트](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>StackExchange.Redis 모범 사례
* 설정 `AbortConnect` toofalse, 후자의 경우 나중에 hello ConnectionMultiplexer 자동으로 다시 연결 합니다. [자세한 내용을 보려면 여기를 참조하세요](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Hello ConnectionMultiplexer reuse-각 요청에 대 한 새를 만들지 마십시오. hello `Lazy<ConnectionMultiplexer>` 패턴 [여기에 표시 된](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) 것이 좋습니다.
* Redis는 더 작은 값에서 가장 잘 작동하므로 더 큰 데이터를 여러 개의 키로 분할하는 것을 고려합니다. [이 Redis 토론](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)에서 100KB는 큰 것으로 간주합니다. 큰 값을 사용할 때 야기될 수 있는 문제 예에 대해서는 [이 문서](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) 를 읽어보세요.
* 구성 프로그램 [스레드 풀 설정](#important-details-about-threadpool-growth) tooavoid 시간 제한입니다.
* 사용에는 적어도 5 초의 기본 connectTimeout hello 합니다. 이 간격에 게 충분 한 시간 toore StackExchange.Redis 부여-네트워크 문제가 발생할 경우 hello 연결을 설정 합니다.
* 실행 중인 다른 작업과 관련 된 hello 성능 비용을 고려해 야 합니다. 예를 들어 hello `KEYS` 명령은 o (n) 작업이 며 피해 야 합니다. hello [redis.io 사이트](http://redis.io/commands/) 주위 hello 시간 복잡도 지 원하는 각 작업에 대 한 세부 정보를 포함 합니다. 각 작업에 대 한 각 명령 toosee hello 복잡성을 클릭 합니다.

#### <a name="configuration-and-concepts"></a>구성 및 개념
* 프로덕션 시스템에 대해 표준 또는 프리미엄 계층을 사용합니다. hello 기본 계층은 단일 노드 시스템 없는 데이터 복제 및 SLA는 없습니다. 또한 C1 이상의 캐시를 사용합니다. C0 캐시는 일반적으로 간단한 개발/테스트 시나리오에 사용됩니다.
* Redis는 **메모리 내** 데이터 저장소입니다. 데이터 손실이 발생할 수 있는 시나리오에 대해서는 [이 문서](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) 를 읽어보세요.
* 연결 탐사 처리할 수 있도록 시스템을 개발 [기한 toopatching 및 장애 조치](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md)합니다.

#### <a name="performance-testing"></a>성능 테스트
* 사용 하 여 시작 `redis-benchmark.exe` tooget 자체 성능 테스트를 작성 하기 전에 가능한 처리량에 대 한 느낌 합니다. 때문에 `redis-benchmark` SSL을 지원 하지 않습니다 해야 [hello Azure 포털을 통해 hello 비 SSL 포트를 사용 하도록 설정](cache-configure.md#access-ports) hello 테스트를 실행 하기 전에. 예제를 보려면 [어떻게 있습니까 벤치 마크 하 고 테스트할 수 내 캐시의 성능을 hello?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* hello VM 테스트에 사용 되는 클라이언트 hello에 있어야 합니다. Redis 캐시 인스턴스의와 동일한 영역입니다.
* Hello 최상의 결과 제공 해야 하 고 더 나은 하드웨어를 가진 클라이언트에 대 한 Dv2 VM 시리즈를 사용 하는 것이 좋습니다.
* 선택한 VM에 그 이상의 컴퓨팅 요구 및 대역폭 기능이 테스트 하는 hello 캐시 클라이언트에 있는지 확인 하십시오.
* 사용 중인 Windows hello 클라이언트 컴퓨터에서 VRSS를 설정 합니다. [자세한 내용을 보려면 여기를 참조하세요](https://technet.microsoft.com/library/dn383582.aspx).
* 프리미엄 계층 Redis 인스턴스는 CPU와 네트워크 모두 더 나은 하드웨어에서 실행되므로 더 우수한 네트워크 대기 시간 및 처리량을 제공합니다.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>무엇 인가요 일반적인 Redis 명령을 사용 하는 경우 몇 가지 고려 사항 hello?
* 이러한 명령의 hello 영향을 이해 하지 않고 오랫동안 toocomplete 시간은 특정 Redis 명령을 실행 하지 마십시오.
  * 예를 들어 hello를 실행 하지 마십시오 [키](http://redis.io/commands/keys) 프로덕션 환경에서 명령으로 hello 키 수에 따라 시간이 오래 tooreturn 걸릴 수 있습니다. Redis는 단일 스레드 서버이며 한 번에 하나씩 명령을 처리합니다. 키 후 실행 하는 다른 명령을 설정한 경우은 처리 되지 않습니다 Redis hello 키 명령을 처리할 때까지 합니다. hello [redis.io 사이트](http://redis.io/commands/) 주위 hello 시간 복잡도 지 원하는 각 작업에 대 한 세부 정보를 포함 합니다. 각 작업에 대 한 각 명령 toosee hello 복잡성을 클릭 합니다.
* 키 크기 - 작은 키/값을 사용해야 하나요, 아니면 큰 키/값을 사용해야 하나요? 일반적으로 hello 시나리오에 따라 다릅니다. 큰 키를 해야 하는 시나리오를 있습니다 수 ConnectionTimeout hello를 조정 하 고 다시 시도 값을 조정 재시도 논리 합니다. Redis 서버 측면에서 값이 작을수록 더 나은 성능은 toohave 적용 됩니다.
* 이러한 고려 사항은 Redis;에 값이 클수록를 저장할 수 없습니다 것을 의미 하지 않습니다. hello 다음 고려 사항에 주의 해야 합니다. 대기 시간이 더 길어집니다. 큰 데이터 집합이 고 다른 하나에 작은 설정한 경우 여러 ConnectionMultiplexer 인스턴스를 사용할 수 있는데, hello 이전에 설명 된 대로 다른 제한 시간 및 재시도 값 집합으로 구성 하는 각 [hello 않는 기능 StackExchange.Redis 구성 옵션 대신할](#cache-configuration) 섹션.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>어떻게 하나요 벤치 마크 하 고 테스트할 수 내 캐시의 성능을 hello?
* [캐시 진단을 사용 하도록 설정](cache-how-to-monitor.md#enable-cache-diagnostics) 할 수 있도록 [모니터](cache-how-to-monitor.md) hello 캐시의 상태입니다. Hello 수도 hello Azure 포털에서 메트릭을 볼 수 있습니다 [다운로드 하 여 검토](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 선택한 hello 도구를 사용 하 게 합니다.
* Redis 서버 redis benchmark.exe tooload 테스트를 사용할 수 있습니다.
* 부하 테스트 클라이언트 hello 및 hello Redis 캐시 hello에 있는지 확인 하세요 동일한 지역입니다.
* Redis cli.exe를 사용 하 고 hello 정보 명령을 사용 하 여 hello 캐시를 모니터링 합니다.
* 부하 높은 메모리 조각화를 발생 시킨 tooa 더 큰 캐시 크기를 조정 해야 합니다.
* Hello 다운로드 방법은 Redis 도구, 참조 hello [Redis 명령을 실행 하는 방법?](#cache-commands) 섹션.

hello 다음 명령은 제공 benchmark.exe redis를 사용 하는 예제입니다. 정확한 결과 위해 hello VM에서 다음이 명령을 실행 하면 캐시와 동일한 지역입니다.

* 1K 페이로드를 사용하여 파이프라인 SET 요청 테스트

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* 1K 페이로드를 사용하여 파이프라인 GET 요청 테스트
  참고: 첫 번째 toopopulate 캐시 위에 표시 된 hello 집합 테스트 실행

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>ThreadPool 증가에 대한 중요한 세부 정보
hello CLR 스레드 풀에 두 가지 유형의 스레드-"작업자" 및 "I/O 완료 포트" (즉, IOCP) 스레드입니다.

* 작업자 스레드는 `Task.Run(…)` 또는 `ThreadPool.QueueUserWorkItem(…)` 메서드 처리 등을 할 경우 사용됩니다. 이러한 스레드 작업 백그라운드 스레드에서 toohappen 해야 할 때에 hello CLR 다양 한 구성 요소에 의해 사용 됩니다.
* IOCP 스레드는 비동기 IO (예: hello 네트워크에서 읽기) 경우에 사용 됩니다.

hello 스레드 풀은 새 작업자 스레드 또는 I/O 완료 스레드 될 때까지 (모든 제한) 없이 필요에 따라 각 유형의 스레드에 대 한 hello "최소" 설정에 도달 합니다. 기본적으로 hello 최소 스레드 수는 시스템에서 프로세서 toohello 수가 설정 됩니다.

한 번 hello 수가 "기존 (사용 중인) 스레드 적중 hello 최소" 스레드 수, hello ThreadPool 됩니다 스로틀 hello 속도 500 밀리초 당 새 스레드 tooone 스레드 삽입입니다. 일반적으로 시스템에서는 IOCP 스레드가 필요한 작업이 폭주하면 해당 작업을 매우 신속하게 처리합니다. 그러나, 작업의 hello 버스트 hello "최소" 하는 설정을 구성 하는 보다 큰 경우 hello ThreadPool 대기로 다음 두 가지 toohappen 중 하나에 대 한 처리 hello 작업의 일부에 약간 시간이 걸릴 수 있습니다.

1. 기존 스레드 무료 tooprocess hello 작업 됩니다.
2. 500ms에 대해 기존 스레드를 사용할 수 없으므로 새 스레드가 만들어집니다.

기본적으로,는 hello 사용 중인 스레드 수가 최소 스레드 수 보다 큰 경우 가능성이 결제 하는 500ms 지연 hello 응용 프로그램에서 네트워크 트래픽을 처리 하기 전에 의미 합니다. 또한 것이 중요 한 toonote 기존 때 스레드 됩니다 (기억 I에 기반)은 15 초 보다 오랫동안 유휴 상태 정리 합니다 하 고 발생 한 증가 및 감소의이 주기를 반복할 수 있습니다.

StackExchange.Redis(빌드 1.0.450 이상)의 예제 오류 메시지를 살펴보는 경우 ThreadPool 통계를 인쇄하는 것을 볼 수 있습니다(아래 IOCP 및 작업자 세부 정보 참조).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

Hello 이전 예제에서는 IOCP 스레드는 6 사용 중인 스레드 및 hello 시스템은 구성 된 tooallow 4 최소 스레드를 볼 수 있습니다. 이 경우 hello 클라이언트 가능성이 했겠지만 두 500 밀리초의 지연이 발생 하기 때문에 6 > 4.

IOCP 또는 작업자 스레드의 증가에 제한이 있는 경우 StackExchange.Redis는 시간 제한에 도달할 수 있습니다.

### <a name="recommendation"></a>권장 사항
이 정보는 고객 설정 좋습니다 hello 최소 구성 값에 대 한 IOCP 및 작업자 스레드 toosomething hello 기본값 보다 큰 합니다. 에서는 하나의 응용 프로그램에 알맞은 값 hello를 다른 응용 프로그램에 대 한 너무 높은/낮은 수 때문에이 값은 이어야에 일괄적으로 적용할 지침을 제공할 수 없습니다. 이 설정은 각 고객 toofine 조정 특정 설정을 tootheir이 필요 하므로 hello 성능 복잡 한 응용 프로그램의 다른 부분에 영향이 미칠 수 있습니다. 좋은 시작 지점은 200 또는 300이며 필요에 따라 테스트 및 조정합니다.

어떻게 tooconfigure이이 설정:

* Asp.net에서 사용 하 여 hello ["minIoThreads" 구성 설정] [ "minIoThreads" configuration setting] hello 아래 `<processModel>` web.config에 구성 요소입니다. Azure 웹 사이트 내에서 실행 하는 경우이 설정은 hello 구성 옵션을 통해 노출 되지 않습니다. 하지만 사용자는 여전히 해야 프로그래밍 방식으로이 설정 수 tooconfigure 수 (아래 참조)에서 global.asax.cs Application_Start 메서드에서 합니다.

  > [!NOTE] 
  > hello이 구성 요소에 지정 된 값은 한 *당 코어* 설정 합니다. 예를 들어 4 코어 컴퓨터 있고 런타임 시 프로그램 minIOThreads 설정 toobe 200을 원하는 경우 사용 `<processModel minIoThreads="50"/>`합니다.
  >

* ASP.NET 외부에서 사용 하 여 hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API입니다.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>StackExchange.Redis를 사용 하는 경우 서버 GC tooget hello 클라이언트에서 더 많은 처리량을 사용
서버 GC 활성화를 최적화할 수 hello 클라이언트 StackExchange.Redis를 사용 하는 경우 향상 된 성능 및 처리량을 제공 합니다. 서버 GC에 대 한 자세한 내용은 방법을 tooenable, hello 다음 문서를 참조 하세요.

* [tooenable 서버 GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [가비지 수집 기본 사항](https://msdn.microsoft.com/library/ee787088.aspx)
* [가비지 수집 및 성능](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>연결에 대한 성능 고려 사항

가격 책정 계층마다 클라이언트 연결, 메모리 및 대역폭에 대한 제한이 다릅니다. 각 캐시 크기를 허용 하지만 *최대* 연결의 특정 수, 각 연결 tooRedis 오버 헤드가 연결 되어 있습니다. 이러한 오버헤드의 예로 TLS/SSL 암호화의 결과인 CPU 및 메모리 사용량이 있습니다. 특정된 캐시 크기에 대 한 최대 연결 제한 hello 부하가 적은 캐시를 가정합니다. 하는 경우 연결 오버 헤드가에서 로드할 *플러스* hello 시스템에 대 한 용량을 초과 하는 클라이언트 작업에서의 로드, hello 현재 캐시 크기에 대 한 hello 연결 제한을 초과한 경우에 hello 캐시 용량 문제가 발생할 수 있습니다.

각 계층에 대 한 hello 서로 다른 연결 제한에 대 한 자세한 내용은 참조 [Azure Redis Cache 가격](https://azure.microsoft.com/pricing/details/cache/)합니다. 연결 및 기타 기본 구성에 대한 정보는 [기본 Redis 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요.

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>내 캐시의 hello 상태와 성능을 모니터링 하려면 어떻게 해야 합니까?
Hello에서 Microsoft Azure Redis 캐시 인스턴스를 모니터링할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 볼 메트릭, 메트릭 차트 toohello 시작 보드에 고정, 모니터링 차트의 hello 날짜 및 시간 범위를 사용자 지정, 추가 및 hello 차트에서 메트릭을 제거 있고 특정 조건이 충족 될 때 경고를 설정 합니다. 자세한 내용은 [Azure Redis Cache 모니터링](cache-how-to-monitor.md)을 참조하세요.

Redis Cache hello **리소스 메뉴** 도 모니터링 및 캐시 문제 해결에 대 한 여러 가지 도구를 포함 합니다.

* **문제 진단 및 해결**에서는 일반적인 문제 및 문제 해결 전략에 대한 정보를 제공합니다.
* **리소스 상태** 기능은 리소스를 감시하고 예상대로 실행되는지를 알려줍니다. Hello Azure 리소스 상태 관리 서비스에 대 한 자세한 내용은 참조 [Azure 리소스 상태 개요](../resource-health/resource-health-overview.md)합니다.
* **새로운 지원 요청** 캐시에 대 한 옵션 tooopen 지원 요청을 제공 합니다.

이러한 도구는 하면 toomonitor hello 상태 Azure Redis 캐시 인스턴스를 사용 하도록 설정 하 고 캐싱 응용 프로그램을 관리 하는 데 도움이 됩니다. 자세한 내용은의 hello "지원 및 문제 해결 설정" 섹션을 참조 하십시오. [어떻게 tooconfigure Azure Redis 캐시](cache-configure.md)합니다.

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>왜 시간 초과가 표시되나요?
시간 제한을 tootalk tooRedis를 사용 하는 hello 클라이언트에서 발생 합니다. 명령을 toohello Redis 서버에 전송 될 때 hello 명령을 큐에 저장 되 고 Redis 서버 hello 명령.wadcfg 해당 명령을 실행 합니다. 그러나이 프로세스 동안 시간 초과 및 예외가 그렇게 되 면 hello 클라이언트 수는 발생 hello 측면을 호출 합니다. 시간 초과 문제를 해결하는 방법에 대한 자세한 내용은 [클라이언트 쪽 문제 해결](cache-how-to-troubleshoot.md#client-side-troubleshooting) 및 [StackExchange.Redis 시간 초과 예외](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions)를 참조하세요.

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>클라이언트는 hello 캐시에서 연결이 끊어진 이유는?
캐시 연결 끊기에 대 한 몇 가지 일반적인 이유는 hello 다음과가 같습니다.

* 클라이언트 쪽 원인
  * hello 클라이언트 응용 프로그램을 다시 배포 했습니다.
  * 크기 조정 작업을 수행 하는 hello 클라이언트 응용 프로그램입니다.
    * 클라우드 서비스 또는 웹 응용 프로그램의 경우 hello 때문일 수 있으므로 tooauto 크기 조정 합니다.
  * 네트워킹 계층 변경 hello 클라이언트 쪽에서 hello 합니다.
  * 일시적인 오류 hello 클라이언트와 서버 hello hello 네트워크 노드 또는 hello 클라이언트에서 발생 했습니다.
  * hello 대역폭 임계값 제한에 도달 했습니다.
  * CPU 바인딩된 작업 toocomplete 너무 오래 걸렸습니다.
* 서버 쪽 원인
  * Hello 표준 캐시 기능에서 hello Azure Redis 캐시 서비스는 hello 주 노드 toohello 보조 노드에서 장애 조치를 시작 합니다.
  * Azure는 hello 캐시 배포 된 hello 인스턴스를 패치 되었습니다.
    * 이 작업은 Redis 서버 업데이트 또는 일반적인 VM 유지 관리를 위한 것일 수 있습니다.

### <a name="which-azure-cache-offering-is-right-for-me"></a>내게 적합한 Azure 캐시 기능
> [!IMPORTANT]
> 작년 [공지](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)에 따라 Azure Managed Cache Service 및 Azure In-Role Cache Service가 2016년 11월 30일에 **중지되었습니다**. 권장 하는 것은 toouse [Azure Redis Cache](https://azure.microsoft.com/services/cache/)합니다. 마이그레이션하는 방법에 대 한 정보를 참조 하십시오. [관리 캐시 서비스 tooAzure Redis Cache에서에서 마이그레이션](cache-migrate-to-redis.md)합니다.
>
>

### <a name="azure-redis-cache"></a>Azure Redis 캐시(영문)
Azure Redis 캐시 크기로 too53 GB 일반적으로 사용할 수 있고 99.9%의 가용성 SLA를 보유 합니다. 새 hello [premium 계층](cache-premium-tier-intro.md) 크기 too530 GB 및 VNET 및 지 속성, SLA 99.9% 클러스터링에 대 한 지원을 제공 합니다.

Azure Redis 캐시 제공 고객 hello 기능 toouse는 안전한 전용 Redis 캐시를 Microsoft에서 관리 합니다. 이 통해 tooleverage hello 다양 한 기능 집합 및 Redis에서의 안정적인 호스팅 및 모니터링 Microsoft에서 제공한 생태계를 얻습니다.

Redis는 키 값 쌍만 다루는 기존 캐시와 달리 높은 성능의 데이터 형식 때문에 널리 사용됩니다. 또한 redis는 tooa 문자열; 추가 처럼 이러한 형식에 원자성 작업을 실행 하는 지원 해시;에서 hello 값 증가 푸시 tooa 목록으로 나타납니다. 교집합, 합집합 및 차집합을 계산 또는 정렬된 된 집합에서 순위가 가장 높은 가져오는 hello 멤버입니다. 다른 기능에는 트랜잭션, pub/sub, Lua 스크립팅,-time-to-live, 제한 된 키에 대 한 지원을 포함 하 고 Redis 하 게 동작 하는 구성 설정을 toomake가 기존 캐시와 유사 합니다.

또 다른 중요 한 사항 tooRedis 성공을 hello 유익한 오픈 소스 에코 시스템입니다. 여러 언어로 hello Redis 클라이언트를 사용할 수 있는 다양 한 집합에 반영 됩니다. 이 에코 시스템 및 클라이언트의 다양 한 범위의 거의 Azure 내에서 구축 하는 모든 작업에서 사용 하는 Azure Redis Cache toobe를 허용 합니다.

Azure Redis Cache 시작 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooUse Azure Redis 캐시](cache-dotnet-how-to-use-azure-redis-cache.md) 및 [Azure Redis Cache 설명서](index.md)합니다.

### <a name="managed-cache-service"></a>관리된 캐시 서비스
[Managed Cache Service는 2016년 11월 30일에 사용이 중지되었습니다.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)(영문)

tooview 보관 설명서 참조 [보관 된 관리 캐시 서비스 설명서](https://msdn.microsoft.com/library/azure/dn386094.aspx)합니다.

### <a name="in-role-cache"></a>In-Role Cache
[In-Role Cache는 2016년 11월 30일에 사용이 중지되었습니다.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)(영문)

tooview 보관 설명서 참조 [보관 된 역할 내 캐시 설명서](https://msdn.microsoft.com/library/azure/dn386103.aspx)합니다.

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx

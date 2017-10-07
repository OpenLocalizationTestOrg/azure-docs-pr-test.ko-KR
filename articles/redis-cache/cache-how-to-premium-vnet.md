---
title: "aaaConfigure Premium Azure Redis Cache에 대 한 가상 네트워크 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 및 프리미엄 계층 Azure Redis 캐시 인스턴스에 대 한 지원 가상 네트워크를 관리 합니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>가상 네트워크를 tooconfigure Premium Azure Redis Cache에 대해 지원 되는 방법
Azure Redis 캐시 캐시 크기 및 기능, 프리미엄 계층 기능 클러스터링, 지 속성 및 가상 네트워크 지원 등을 포함 하 여 hello 선택에서 유연성을 제공 하는 다른 캐시 기능에 있습니다. VNet은 hello 클라우드에서 개인 네트워크입니다. Azure Redis Cache 인스턴스 VNet를 구성 된 경우 공개적으로 주소 지정 가능한 아니며 가상 컴퓨터 및 hello VNet 내에서 응용 프로그램에서 액세스할 수 있습니다. 이 문서에서는 tooconfigure 가상 네트워크는 프리미엄 Azure Redis 캐시 인스턴스에 대 한 지원 되는 방법을 설명 합니다.

> [!NOTE]
> Azure Redis Cache는 클래식 및 Resource Manager VNet을 둘 다 지원합니다.
> 
> 

다른 프리미엄 캐시 기능에 대 한 자세한 내용은 참조 [toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)합니다.

## <a name="why-vnet"></a>VNet을 사용하는 이유
[Azure 가상 네트워크 (VNet)](https://azure.microsoft.com/services/virtual-network/) 배포에서는 강화 된 보안 및 액세스 제어 정책 서브넷 뿐 Azure Redis Cache에 대 한 격리 및 기타 기능 toofurther 액세스를 제한 합니다.

## <a name="virtual-network-support"></a>가상 네트워크 지원
가상 네트워크 (VNet) 지원이 hello에 구성 된 **새 Redis 캐시** 블레이드 캐시 만들기 중입니다. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Hello에 있는 VNet을 선택 하 여 Redis VNet 통합을 구성할 수는 프리미엄 가격 책정 계층을 선택 하면 동일한 구독 및 캐시에 위치 합니다. toouse 새 VNet에 hello 단계에 따라 것을 먼저 만든 [hello Azure 포털을 사용 하 여 가상 네트워크를 만들고](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 또는 [hello Azure 포털을 사용 하 여 가상 네트워크 (클래식)를 만들](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) toohello 다음 다시 돌아와 **새 Redis 캐시** 블레이드 toocreate 및 프리미엄 캐시를 구성 합니다.

새 캐시에 대 한 tooconfigure hello VNet 클릭 **가상 네트워크** hello에 **새 Redis 캐시** 블레이드에서 하 고 선택 hello VNet hello 드롭 다운 목록에서 원하는 합니다.

![가상 네트워크][redis-cache-vnet]

선택 hello hello에서 원하는 서브넷 **서브넷** 드롭 다운 목록 및 원하는 hello 지정 **고정 IP 주소**합니다. 클래식 VNet hello를 사용 하는 경우 **고정 IP 주소** 필드는 선택 사항이 고 지정 되지 않은 경우 선택한 hello 서브넷에서 선택 됩니다 하나입니다.

> [!IMPORTANT]
> Azure Redis Cache tooa 리소스 관리자 VNet을 배포할 때는 hello 캐시 Azure Redis 캐시 인스턴스를 제외 하 고 다른 리소스가 없는 포함 하는 전용된 서브넷에 있어야 합니다. Toodeploy 하려고 시도 하는 경우 Azure Redis Cache tooa 다른 리소스, hello 배포를 포함 하는 리소스 관리자 VNet tooa 서브넷 실패 합니다.
> 
> 

![가상 네트워크][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure는 각 서브넷 내의 일부 IP 주소를 예약하며, 이러한 주소는 사용할 수 없습니다. hello hello 서브넷의 첫 번째 및 마지막 IP 주소가 예약 되어 Azure 서비스에 사용 되는 3 개 더 많은 주소와 함께 프로토콜 적합성을 위해 있습니다. 자세한 내용은 [이러한 서브넷 내에서 IP 주소를 사용하는데 제한 사항이 있습니까?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> 또한 toohello IP 주소에서 hello Azure VNET 인프라에서 사용 하는 각 Redis 영역당 hello 서브넷 2 사용 하 여 IP 주소 및 hello 부하 분산 장치에 대 한 하나의 추가 IP 주소 인스턴스. 클러스터 되지 않은 캐시 toohave 하나의 분할 영역으로 간주 됩니다.
> 
> 

Hello 캐시를 만든 후를 클릭 하 여 hello VNet에 대 한 hello 구성을 볼 수 있습니다 **가상 네트워크** hello에서 **리소스 메뉴**합니다.

![가상 네트워크][redis-cache-vnet-info]

다음 예제는 hello와 같이 hello 연결 문자열에 hello 호스트 이름 캐시를 지정 하는 tooconnect tooyour Azure Redis 캐시 인스턴스에 VNet을 사용 하는 경우:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Azure Redis Cache VNet FAQ
다음 목록 hello hello Azure Redis 캐시 크기 조정에 대 한 질문과 대답 toocommonly 포함 되어 있습니다.

* [Azure Redis Cache 및 VNet의 몇 가지 일반적인 구성 오류 문제는 무엇인가요?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [캐시가 VNET에서 작동하는지 확인하려면 어떻게 해야 하나요?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [표준 또는 기본 캐시에 VNet을 사용할 수 있나요?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [일부 서브넷에서만 Redis Cache 생성이 실패하는 이유는 무엇인가요?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Hello 서브넷 주소 공간 요구 사항은 무엇입니까?](#what-are-the-subnet-address-space-requirements)
* [VNET에서 캐시를 호스팅하는 경우 모든 캐시 기능이 작동하나요?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Azure Redis Cache 및 VNet의 몇 가지 일반적인 구성 오류 문제는 무엇인가요?
Azure Redis Cache는 VNet에서 호스트 되는 경우 다음 표는 hello에 hello 포트 사용 됩니다. 

>[!IMPORTANT]
>다음 표에서 hello에서 hello 포트 차단 되 면 hello 캐시 제대로 작동 하지 않을 수 있습니다. VNet에서 Azure Redis Cache를 사용 하는 경우 hello 가장 일반적인 구성 오류 문제는 하나 또는이 포트를 차단 합니다.
> 
> 

- [아웃바운드 포트 요구 사항](#outbound-port-requirements)
- [인바운드 포트 요구 사항](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>아웃바운드 포트 요구 사항

7가지 아웃바운드 포트 요구 사항이 있습니다.

- 원하는 경우 인터넷 클라이언트의를 통해 가능 모든 아웃 바운드 연결 toohello 온-프레미스 감사 장치입니다.
- Azure 저장소 및 Azure DNS 서비스는 트래픽을 tooAzure 끝점 경로 hello 포트 중 3 개.
- 포트 범위를 남은 hello 및 내부 Redis 서브넷 통신에 대 한 합니다. 내부 Redis 서브넷 통신에 필요한 서브넷 NSG 규칙은 없습니다.

| 포트 | 방향 | 전송 프로토콜 | 목적 | 로컬 IP | 원격 IP |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |아웃바운드 |TCP |Azure 저장소/PKI(인터넷)에 대한 Redis 종속성 | (Redis 서브넷) |* |
| 53 |아웃바운드 |TCP/UDP |DNS(인터넷/VNet)에 대한 Redis 종속성 | (Redis 서브넷) |* |
| 8443 |아웃바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) | (Redis 서브넷) |
| 10221-10231 |아웃바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) | (Redis 서브넷) |
| 20226 |아웃바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷) |
| 13000-13999 |아웃바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷) |
| 15000-15999 |아웃바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷) |


### <a name="inbound-port-requirements"></a>인바운드 포트 요구 사항

8개의 인바운드 포트 범위 요구 사항이 있습니다. 이 범위에 대 한 인바운드 요청은 인바운드 hello에서 호스팅되는 다른 서비스를 같은 VNET 또는 내부 toohello Redis 서브넷 통신 합니다.

| 포트 | 방향 | 전송 프로토콜 | 목적 | 로컬 IP | 원격 IP |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |인바운드 |TCP |클라이언트 통신 tooRedis Azure 부하 분산 | (Redis 서브넷) |가상 네트워크, Azure Load Balancer |
| 8443 |인바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷) |
| 8500 |인바운드 |TCP/UDP |Azure 부하 분산 | (Redis 서브넷) |Azure Load Balancer |
| 10221-10231 |인바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷), Azure Load Balancer |
| 13000-13999 |인바운드 |TCP |클라이언트 통신 tooRedis Azure 부하 분산 클러스터 | (Redis 서브넷) |가상 네트워크, Azure Load Balancer |
| 15000-15999 |인바운드 |TCP |클라이언트 통신 tooRedis 클러스터의 경우 Azure 부하 분산 | (Redis 서브넷) |가상 네트워크, Azure Load Balancer |
| 16001 |인바운드 |TCP/UDP |Azure 부하 분산 | (Redis 서브넷) |Azure Load Balancer |
| 20226 |인바운드 |TCP |Redis에 대한 내부 통신 | (Redis 서브넷) |(Redis 서브넷) |

### <a name="additional-vnet-network-connectivity-requirements"></a>추가 VNET 네트워크 연결 요구 사항

가상 네트워크에서 처음에 충족되지 않는 Azure Redis Cache에 대한 네트워크 연결 요구 사항이 있습니다. Azure Redis Cache는 가상 네트워크에서 사용 될 때 제대로 항목 toofunction 다음 hello 모두 필요 합니다.

* 아웃 바운드 네트워크 연결 tooAzure 저장소 끝점 전 세계입니다. Hello에 있는 끝점 여기에 동일한 지역에 있는 저장소 끝점 뿐만 아니라 hello Azure Redis Cache 인스턴스 **다른** Azure 지역입니다. Azure 저장소 끝점 hello 다음 DNS 도메인에서 해결: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*, 및 *file.core.windows.net*합니다. 
* 아웃 바운드 네트워크 연결이 너무*ocsp.msocsp.com*, *mscrl.microsoft.com*, 및 *crl.microsoft.com*합니다. 이 연결이 필요한 toosupport SSL 기능에 설명 합니다.
* hello 가상 네트워크에 대 한 DNS 구성을 hello 모든 hello 끝점 확인 가능한 수 있어야 하며 도메인에 언급 된 hello 이전 포인트입니다. 유효한 DNS 인프라를 구성 하 고 hello 가상 네트워크에 대 한 유지 관리 함으로써 이러한 DNS 요구 사항은 충족할 수 있습니다.
* 다음 DNS 도메인 hello에서 해결 하는 Azure 모니터링 끝점을 다음 아웃 바운드 네트워크 연결 toohello: shoebox2 black.shoebox2.metrics.nsatc.net, 북부-prod2.prod2.metrics.nsatc.net azglobal black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net 동부-prod2.prod2.metrics.nsatc.net azglobal red.azglobal.metrics.nsatc.net 합니다.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>캐시가 VNET에서 작동하는지 확인하려면 어떻게 해야 하나요?

>[!IMPORTANT]
>VNET에 호스트 된 tooan Azure Redis 캐시 인스턴스를 연결할 때 캐시 클라이언트에 있어야 합니다. 모든 테스트 응용 프로그램 또는 핑 진단 도구를 포함 하 여 동일한 VNET hello 합니다.
>
>

Hello 포트 요구 사항 hello 이전 섹션에 설명 된 대로 구성 되 면 캐시 hello 다음 단계를 수행 하 여 작동 하는지 확인할 수 있습니다.

- [다시 부팅](cache-administration.md#reboot) hello의 모든 노드를 캐시 합니다. Hello의 모든 필수 캐시 종속성에 연결할 수 없습니다 (에 설명 된 대로 [인바운드 포트 요구 사항](cache-how-to-premium-vnet.md#inbound-port-requirements) 및 [아웃 바운드 포트 요구 사항](cache-how-to-premium-vnet.md#outbound-port-requirements)), hello 캐시 수 toorestart를 확인할 수 없습니다.
- Hello 캐시 노드를 다시 시작한 (대로 hello Azure 포털에서에서 hello 캐시 상태 보고) 되 면 hello 다음 테스트를 수행할 수 있습니다.
  - hello 캐시 끝점 (포트 6380 사용) hello 내에 있는 컴퓨터에서 ping 동일한 VNET hello로 사용 하 여 캐시 [tcping](https://www.elifulkerson.com/projects/tcping.php)합니다. 예:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    경우 hello `tcping` hello 포트가 열려, hello 캐시는 hello VNET에 있는 클라이언트에서 연결에 사용할 수 있는 도구를 보고 합니다.

  - 또 다른 방법은 tootest toocreate 테스트 캐시 클라이언트는 (간단한 될 수 있는 StackExchange.Redis를 사용 하 여 콘솔 응용 프로그램) toohello 캐시 연결 하 고 추가 하 고 hello 캐시에서 일부 항목을 검색 합니다. Hello 샘플 클라이언트 응용 프로그램에 있는 VM에 설치 hello 캐시로 동일한 VNET hello 및 tooverify 연결 toohello 캐시를 실행 합니다.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>표준 또는 기본 캐시에 VNet을 사용할 수 있나요?
VNet은 프리미엄 캐시에만 사용할 수 있습니다.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>일부 서브넷에서만 Redis Cache 생성이 실패하는 이유는 무엇인가요?
Azure Redis Cache tooa 리소스 관리자 VNet에 배포 하는 경우에 hello 캐시 다른 리소스 형식을 포함 하는 전용된 서브넷에 있어야 합니다. Toodeploy 하려고 시도 하는 경우 Azure Redis Cache tooa 다른 리소스, hello 배포를 포함 하는 리소스 관리자 VNet 서브넷 실패 합니다. 새 Redis 캐시를 만들기 전에 hello hello 서브넷 내의 기존 리소스를 삭제 해야 합니다.

여러 유형을 배포할 수의 리소스 tooa 클래식 VNet으로 충분 한 IP는 사용할 수 있는 주소입니다.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Hello 서브넷 주소 공간 요구 사항은 무엇입니까?
Azure는 각 서브넷 내의 일부 IP 주소를 예약하며, 이러한 주소는 사용할 수 없습니다. hello hello 서브넷의 첫 번째 및 마지막 IP 주소가 예약 되어 Azure 서비스에 사용 되는 3 개 더 많은 주소와 함께 프로토콜 적합성을 위해 있습니다. 자세한 내용은 [이러한 서브넷 내에서 IP 주소를 사용하는데 제한 사항이 있습니까?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

또한 toohello IP 주소에서 hello Azure VNET 인프라에서 사용 하는 각 Redis 영역당 hello 서브넷 2 사용 하 여 IP 주소 및 hello 부하 분산 장치에 대 한 하나의 추가 IP 주소 인스턴스. 클러스터 되지 않은 캐시 toohave 하나의 분할 영역으로 간주 됩니다.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>VNET에서 캐시를 호스팅하는 경우 모든 캐시 기능이 작동하나요?
캐시는 VNET의 일부 이면 hello 캐시 hello VNET에서에서 클라이언트에만 액세스할 수 있습니다. 결과적으로, hello 다음 캐시 관리 기능이 작동 하지 않는이 이번에 있습니다.

* Redis 콘솔-tooyour 캐시 Redis 콘솔 hello VNET 외부에 있는 로컬 브라우저에서 실행 되기 때문에 연결할 수 없는 합니다.

## <a name="use-expressroute-with-azure-redis-cache"></a>Azure Redis Cache에서 Express 경로 사용
고객 연결할 수는 [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) 회로 tootheir 가상 네트워크 인프라를 해당 온-프레미스 네트워크 tooAzure 기능을 확장할 합니다. 

기본적으로 새로 만든 ExpressRoute 회로는 VNET에서 강제 터널링(0.0.0.0/0 기본 경로 보급 알림)을 수행하지 않습니다. 따라서 아웃 바운드 인터넷 연결 hello VNET에서 직접 수 있으며 클라이언트 응용 프로그램은 Azure 수 tooconnect tooother 끝점 Azure Redis Cache를 포함 합니다.

그러나 일반적인 고객 구성은 강제 터널링 toouse (기본 경로 보급)는 아웃 바운드 인터넷 트래픽을 tooinstead 흐름 온-프레미스를 강제로 수행 합니다. 이 트래픽 흐름 hello 아웃 바운드 트래픽이 되는 경우 Azure Redis Cache와의 연결을 중단 한 다음을 hello Azure Redis 캐시 인스턴스에 없는 종속성과 함께 수 toocommunicate 온-프레미스를 차단 합니다.

hello 방법은 toodefine 하나 이상의 사용자 정의 된 경로 (UDRs) hello Azure Redis Cache를 포함 하는 hello 서브넷에 있습니다. UDR hello 기본 경로 대신 허용 되어야 하는 서브넷 별 경로 정의 합니다.

가능 하면 같은 구성이 toouse hello를 좋습니다.

* 0.0.0.0/0을 보급 하는 hello ExpressRoute 구성 하 고 기본적으로 강제 터널링 모든 아웃 바운드 트래픽을 온-프레미스 키를 누릅니다.
* hello UDR 적용 toohello 서브넷 hello Azure Redis Cache를 포함 하 정의 된 TCP/IP 트래픽 toohello에 대 한 작업 경로 0.0.0.0/0은 공용 인터넷; 예를 들어 hello 설정 하 여 다음 홉 형식 too'Internet'.

hello 결합 된 효과 이러한 단계는 hello 서브넷 수준은 UDR 우선 hello hello Azure Redis Cache에서에서 아웃 바운드 인터넷에 액세스 하는 데 ExpressRoute 강제 터널링 합니다.

ExpressRoute를 사용 하는 온-프레미스 응용 프로그램에서 연결 tooan Azure Redis Cache 인스턴스 tooperformance 이유로 인해 일반적인 사용 시나리오는 되지 않습니다 (최상의 성능을 얻으려면 Azure Redis Cache에 대 한 클라이언트 hello에 있어야 hello Azure Redis Cache와 동일한 지역).

>[!IMPORTANT] 
>UDR에 정의 된 경로 hello **해야** hello ExpressRoute 구성에서 보급 하는 모든 경로 통해 모호한 tootake 우선 순위 수 있도록 합니다. hello 다음 예제에서는 hello 광범위 한 0.0.0.0/0 주소 범위를 사용 하 여 및 따라서 경로 알림이 더 구체적인 주소 범위를 사용 하 여 실수로 재정의 잠재적으로 수 있습니다.

>[!WARNING]  
>Azure Redis 캐시 된 express 경로 구성 지원 되지 않습니다는 **hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 경로 크로스-보급할 잘못**합니다. 구성된 공용 피어링이 있는 ExpressRoute 구성은 다양한 Microsoft Azure IP 주소 범위 집합에 대해 Microsoft에서 경로 보급을 받습니다. 이러한 주소 범위가 잘못 크로스-에 보급 hello 개인 피어 링 경로 hello 결과 hello Azure Redis 캐시 인스턴스의 서브넷의 모든 아웃 바운드 네트워크 패킷이 됩니다 tooa 잘못 강제 터널링 된 고객의 온-프레미스 네트워크 인프라입니다. 이 네트워크 흐름은 Azure Redis Cache를 중단합니다. hello 솔루션 toothis 문제는 hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 toostop 간 광고 경로입니다.


사용자 정의 경로에 대한 배경 정보는 [개요](../virtual-network/virtual-networks-udr-overview.md)를 참조하세요.

ExpressRoute에 대한 자세한 내용은 [ExpressRoute 기술 개요](../expressroute/expressroute-introduction.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.

* [Toohello Azure Redis Cache 프리미엄 계층 소개](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png


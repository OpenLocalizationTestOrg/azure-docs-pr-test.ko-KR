---
title: "aaaAzure 네트워킹 | Microsoft Docs"
description: "Azure 네트워킹 서비스와 기능에 대해 알아봅니다."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Azure 네트워킹

Azure에서는 함께 또는 별도로 사용할 수 있는 다양한 네트워킹 기능을 제공합니다. Hello에 대 한 더 많은 주요 기능 toolearn 다음 중 하나를 클릭 합니다.
- [Azure 리소스 간의 연결](#connectivity): hello 클라우드에 안전 하 고 개인 가상 네트워크에서 Azure 연결 리소스입니다.
- [인터넷 연결](#internet-connectivity): Azure 리소스에서 tooand hello 인터넷을 통해 통신 합니다.
- [온-프레미스 연결](#on-premises-connectivity): 가상 사설망 (VPN) hello 인터넷을 통해 또는 전용된 연결 tooAzure 통해 온-프레미스 네트워크 tooAzure 리소스를 연결 합니다.
- [부하 분산 및 트래픽 방향](#load-balancing): 동일한 위치와 다른 위치에 직접 트래픽 tooservers에서 부하 분산 트래픽 tooservers hello 합니다.
- [보안](#security): 네트워크 서브넷 또는 개별 VM(가상 컴퓨터) 간에 네트워크 트래픽을 필터링합니다.
- [라우팅](#routing): Azure 및 온-프레미스 리소스 간에 기본 라우팅 또는 전체 제어 라우팅을 사용합니다.
- [관리 효율성](#manageability): Azure 네트워킹 리소스를 모니터링하고 관리합니다.
- [배포 및 구성 도구](#tools): 웹 기반 포털 또는 toodeploy 크로스 플랫폼 명령줄 도구를 사용 하 고 네트워크 리소스를 구성 합니다.

## <a name="Connectivity"></a>Azure 리소스 간 연결

Virtual Machines, Cloud Services, 가상 컴퓨터 확장 집합, Azure App Service 환경과 같은 Azure 리소스는 Azure VNet(가상 네트워크)를 통해 서로 개별적으로 통신할 수 있습니다. VNet hello Azure 클라우드 전용 tooyour의 논리적 격리는 [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다. 각 Azure 구독 및 Azure [지역](https://azure.microsoft.com/regions) 내에서 여러 VNet을 구현할 수 있습니다. 각 VNet은 다른 VNet에서 격리됩니다. 각 VNet에 대해 다음을 수행할 수 있습니다.

- 공용 및 사설(RFC 1918) 주소를 사용하여 사용자 지정 사설 IP 주소 공간을 지정합니다. Azure는 리소스 연결된 toohello VNet 개인 IP 주소를 할당 하는 hello 주소 공간에서 할당 합니다.
- Hello VNet 주소 공간 tooeach 서브넷의 일부를 할당 하 고 hello VNet 하나 이상의 서브넷으로 분할 합니다.
- Azure 제공 이름 확인을 사용 하거나 tooa VNet를 연결 하는 리소스에서 사용 하기 위해 자체 DNS 서버 지정 합니다.

hello Azure 가상 네트워크 서비스를 읽을 hello에 대 한 자세한 toolearn [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서. 다른 Vnet tooeach 연결할 수 있습니다, Vnet에 걸쳐 서로 tooeither VNet toocommunicate 연결 리소스를 사용 하도록 설정 합니다. Hello 옵션 tooconnect Vnet tooeach 다른 다음 중 하나 또는 모두를 사용할 수 있습니다.

- **피어 링:** 사용 리소스 연결 hello 내에서 Azure Vnet toodifferent 서로 동일한 Azure 지역 toocommunicate 합니다. hello 대역폭 및 대기 시간 Vnet은 hello 간에 hello 동일 하면 hello 리소스에 연결 된 toohello 것 처럼 동일한 VNet입니다. 피어 링을 대 한 자세한 toolearn 읽을 hello [가상 네트워크 피어 링 개요](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **VPN 게이트웨이:** 사용 리소스를 서로 toocommunicate 다양 한 Azure 지역 내에서 Azure Vnet toodifferent 연결 합니다. VNet 간의 트래픽은 Azure VPN Gateway를 통해 전송됩니다. Vnet 간 대역폭은 hello 게이트웨이의 제한 toohello 대역폭입니다. hello 읽기는 VPN 게이트웨이 사용 하 여 Vnet를 연결 하는 방법에 대 한 자세한 toolearn [여러 지역 VNet 대 VNet 연결 구성](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

## <a name="internet-connectivity"></a>인터넷 연결

모든 Azure 리소스 연결된 tooa VNet 기본적으로 인터넷 아웃 바운드 연결 toohello가 있어야 합니다. hello hello 리소스의 개인 IP 주소는 원본 네트워크 주소 hello Azure 인프라에 의해 (SNAT) tooa 공용 IP 주소를 변환 합니다. hello 읽을 아웃 바운드 인터넷 연결에 대 한 자세한 toolearn [Azure의 아웃 바운드 연결 이해](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

toocommunicate 인바운드 tooAzure 리소스에서 인터넷을 hello 또는 toocommunicate 아웃 바운드 toohello SNAT, 리소스 없이 인터넷에 공용 IP 주소를 할당 해야 합니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [공용 IP 주소](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

## <a name="on-premises-connectivity"></a>온-프레미스 연결

VPN 연결 또는 직접 개별 연결을 통해 VNet의 리소스 액세스할 수 있습니다. Azure 가상 네트워크와 온-프레미스 네트워크 간에 네트워크 트래픽을 toosend 가상 네트워크 게이트웨이 만들어야 합니다. 연결의 원하는 VPN 또는 express 경로 게이트웨이 toocreate hello 유형 hello에 대 한 설정 구성

온-프레미스 네트워크 tooa hello 다음 옵션을 조합 하 여 VNet을 연결할 수 있습니다.

**지점 및 사이트 간(SSTP를 통한 VPN)**

다음 그림 hello 여러 컴퓨터 사이 VNet에 지점 toosite 별도 연결을 보여 줍니다.

![지점 및 사이트 간](./media/networking-overview/point-to-site.png)

단일 컴퓨터와 VNet 간에 이 연결이 설정됩니다. 이 연결 유형에 거의 또는 전혀 변경 tooyour 기존 네트워크 필요 하기 때문에 수행 하는 개발자를 위한 또는 azure를 하는 경우 유용 합니다. 또한 컨퍼런스 또는 집과 같은 원격 위치에서 연결하는 경우 편리합니다. 지점 및 사이트 연결은 종종 hello 통해 사이트 간 연결과 연결 되어 있으며 동일한 가상 네트워크 게이트웨이. hello 연결 hello 컴퓨터와 hello VNet 간의 인터넷 hello 통한 hello SSTP 프로토콜 암호화 tooprovide 통신을 사용합니다. hello 트래픽이 hello 인터넷에서 이동 하는 지점-사이트 VPN에 대 한 hello 대기 시간은 예측 가능 하지 않습니다.

**사이트 간(IPsec/IKE VPN 터널)**

![사이트 간](./media/networking-overview/site-to-site.png)

온-프레미스 VPN 장치와 Azure VPN Gateway 간에 이 연결이 설정됩니다. 이 연결 유형에 tooaccess hello VNet에 권한을 부여 해야 하는 모든 온-프레미스 리소스를 수 있습니다. hello 연결은 온-프레미스 장치와 hello Azure VPN 게이트웨이 hello 인터넷을 통해 암호화 된 통신을 제공 하는 IPSec/IKE VPN입니다. 여러 온-프레미스 사이트 toohello 연결할 수 같은 VPN 게이트웨이 합니다. hello 온-프레미스 각 사이트에 VPN 장치가 NAT 뒤에 있지 않는 외부 공용 IP 주소가 있어야 합니다. 사이트 간 연결에 대 한 대기 시간 hello은 hello 트래픽이 트래버스하 hello 인터넷 예측 가능 하지 않습니다.

**ExpressRoute(개별 전용 연결)**

![ExpressRoute](./media/networking-overview/expressroute.png)

이 종류의 연결은 ExpressRoute 파트너를 통해 네트워크와 Azure 간에 설정됩니다. 이 연결은 사설 전용입니다. 트래픽 hello 인터넷을 통과 하지 않는 합니다. ExpressRoute 연결에 대 한 hello 대기 시간, 예측 가능한 없으므로 트래픽 hello 인터넷을 트래버스 하지 않습니다. ExpressRoute는 사이트 간 연결과 함께 사용할 수 있습니다.

모든 hello 이전 연결 옵션을 hello 읽기에 대 한 자세한 toolearn [연결 토폴로지 다이어그램](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

## <a name="load-balancing"></a>부하 분산 및 트래픽 방향

Microsoft Azure는 네트워크 트래픽을 분산하고 부하를 분산하는 방법을 관리하는 여러 서비스를 제공합니다. Hello 개별적으로 또는 함께 기능을 다음 중 하나를 사용할 수 있습니다.

**DNS 부하 분산**

hello Azure 트래픽 관리자 서비스가 전역 DNS 부하 분산을 제공합니다. 트래픽 관리자 tooclients hello 라우팅 메서드를 다음 중 하나에 따라 정상 끝점의 hello IP 주소로 응답 합니다.
- **지리:** 클라이언트 toospecific 끝점 (Azure, 외부 또는 중첩 된)에서 시작가 DNS 쿼리에서 지리적 위치에 따라 지정 됩니다. 이 메서드를 사용하면 클라이언트의 지리적 지역을 파악하고 이를 기준으로 라우팅하는 중요한 시나리오를 사용할 수 있습니다. 데이터 독립성 지시 사항, 콘텐츠 및 사용자 환경의 지역화를 준수하고 다른 지역의 트래픽을 측정하는 작업을 예로 들 수 있습니다.
- **성능:** toohello 클라이언트는 hello "가장 가까운" toohello 클라이언트 hello IP 주소가 반환 합니다. hello '가장 가까운' 끝점 지리적 거리를 기준으로 가장 가까운 필요 하지 않습니다. 대신,이 메서드는 네트워크 대기 시간을 측정 하 여 hello 가장 가까운 끝점을 확인 합니다. 트래픽 관리자는 인터넷 대기 시간 테이블 tootrack hello 왕복 시간 IP 주소 범위와 각 Azure 데이터 센터 간에 유지 관리합니다.
- **우선 순위:** 트래픽은 toohello 방향이 지정 된 기본 (가장 높은 우선 순위) 끝점입니다. Hello 기본 끝점에 사용할 수 없는 경우 트래픽 관리자 경로 hello 트래픽 toohello 두 번째 끝점입니다. 두 hello 기본 및 보조 끝점을 사용할 수 없는 경우 세 번째로 등과 hello 트래픽은 toohello를 전송 됩니다. Hello 구성 상태 (사용 또는 사용 하지 않도록 설정)를 기반으로 하는 hello 끝점의 가용성 및 지속적인 끝점 모니터링을 hello 합니다.
- **가중치 적용 라운드 로빈:** Traffic Manager는 각 요청에 대해 사용 가능한 끝점을 임의로 선택합니다. 끝점을 선택할 때의 hello 확률 tooall 사용 가능한 끝점을 할당 하는 hello 가중치를 기반으로 합니다. 모든 끝점 결과도 트래픽 배포에 걸쳐 무게 hello를 사용 하 여 동일 합니다. 특정 끝점에서 위 또는 아래로 가중치를 사용 하 여 해당 끝점 toobe 자주 보내거나 가끔 hello DNS 응답에 반환 하면 됩니다.

hello 다음 그림은 웹 응용 프로그램 보낸 tooa 웹 응용 프로그램 끝점에 대 한 요청입니다. 끝점은 VM 및 Cloud Services와 같은 다른 Azure 서비스일 수도 있습니다.

![트래픽 관리자](./media/networking-overview/traffic-manager.png)

클라이언트 hello toothat 끝점 직접 연결 합니다. Azure 트래픽 관리자 끝점 비정상 이며 클라이언트 tooa 다른, 정상 끝점 리디렉션합니다 경우를 검색 합니다. hello 읽을 트래픽 관리자에서에 대 한 자세한 toolearn [Azure 트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

**응용 프로그램 부하 분산**

hello Azure 응용 프로그램 게이트웨이 서비스는 서비스 응용 프로그램 배달 컨트롤러 ADC ()를 제공합니다. 응용 프로그램 게이트웨이 다양 한 계층 7 (HTTP/HTTPS) 부하 분산 기능 웹 응용 프로그램을 포함 하 여 응용 프로그램에 대 한 방화벽 tooprotect 취약성을 악용 하 여 웹 응용 프로그램을 제공 합니다. 응용 프로그램 게이트웨이 수도 있도록 toooptimize 웹 팜 생산성 CPU를 많이 사용 SSL 종료 toohello 응용 프로그램 게이트웨이 오프 로드 하 여 합니다. 

다른 계층 7 라우팅 기능 들어오는 트래픽을, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅 및 hello 기능 toohost 라운드 로빈 배포는 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트를 포함 합니다. Application Gateway는 인터넷 연결 게이트웨이, 내부 전용 게이트웨이 또는 둘의 조합으로 구성될 수 있습니다. Application Gateway는 전적으로 Azure에 의해 관리되고, 확장성 및 고가용성을 제공합니다. 관리 효율성을 향상시키기 위한 풍부한 진단 및 로깅 기능을 제공합니다. 응용 프로그램 게이트웨이 hello 읽기에 대 한 자세한 toolearn [응용 프로그램 게이트웨이 개요](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

hello 다음 다음과 같은 순서로 URL 경로 기반 응용 프로그램 게이트웨이 라우팅

![응용 프로그램 게이트웨이](./media/networking-overview/application-gateway.png)

**네트워크 부하 분산**

Azure 부하 분산 장치 hello 모든 UDP 및 TCP 프로토콜에 대 한 높은 성능, 짧은 대기 시간 계층 4 부하 분산을 제공합니다. 인바운드 및 아웃 바운드 연결을 관리합니다. 내부 부하가 분산된 공용 끝점을 구성할 수 있습니다. 규칙 toomap 정의한 연결 tooback 엔드 풀 대상 TCP 및 HTTP 상태 검색 옵션 toomanage 서비스 가용성을 사용 하 여 인바운드 합니다. 부하 분산 장치를 읽고 hello에 대 한 자세한 toolearn [부하 분산 장치 개요](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

다음 그림 hello 두 외부 및 내부 부하 분산 장치를 활용 하는 인터넷 연결 다중 계층 응용 프로그램을 보여 줍니다.

![부하 분산 장치](./media/networking-overview/load-balancer.png)

## <a name="security"></a>보안

트래픽 tooand hello 다음 옵션을 사용 하 여 Azure 리소스에서 필터링 할 수 있습니다.

- **네트워크:** Azure 네트워크 보안 그룹 (Nsg) toofilter 인바운드 및 아웃 바운드 구현할 수 tooAzure 리소스 트래픽입니다. 각 NSG는 하나 이상의 인바운드 및 아웃바운드 규칙을 포함합니다. 각 규칙 hello 원본 IP 주소, 대상 IP 주소, 포트 및 프로토콜 트래픽 필터링을 지정 합니다. 적용 된 tooindividual 서브넷 및 개별 Vm에 Nsg 될 수 있습니다. hello 읽을 Nsg에 대 한 자세한 toolearn [네트워크 보안 그룹을 개요](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **응용 프로그램:** 웹 응용 프로그램 방화벽이 설치된 Application Gateway를 사용하여 취약점 및 악용으로부터 웹 응용 프로그램을 보호할 수 있습니다. 일반적인 예로 SQL 주입 공격, 크로스 사이트 스크립팅 및 잘못된 형식의 헤더가 있습니다. Application Gateway는 이 트래픽을 필터링하고 웹 서버에 도달하지 않도록 중지합니다. 사용 하려는 규칙 수 tooconfigure 됩니다. hello 기능 tooconfigure SSL 협상 정책 tooallow 특정 정책 toobe 비활성화 제공 됩니다. hello 읽을 hello 웹 응용 프로그램 방화벽에 대 한 자세한 toolearn [웹 응용 프로그램 방화벽](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

Azure를 제공 및 들은 toouse 네트워크 응용 프로그램을 온-프레미스를 사용 하지 않는 네트워크 기능이 필요한 경우 Vm에서 hello을 구현할 수 있으며 tooyour VNet을 연결할 수 있습니다. hello [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) 네트워크 응용 프로그램을 현재 사용할 수 있는 미리 구성 된 여러 다른 Vm이 포함 됩니다. 미리 구성 된 이러한 Vm은 일반적으로 참조 tooas 네트워크 가상 어플라이언스 (NVA). NVA는 방화벽, WAN 최적화와 같은 응용 프로그램과 함께 사용할 수 있습니다.

## <a name="routing"></a>라우팅

Azure 기본 서로 모든 VNet toocommunicate에서 리소스 연결 된 tooany 서브넷을 사용할 수 있는 경로 테이블을 만듭니다. 구현할 수 있습니다 또는 둘 다의 다음 경로 toooverride 유형의 hello hello Azure 만듭니다 기본 경로:
- **사용자 정의:** 각 서브넷 트래픽이 라우팅된 toofor가 제어 하는 경로 가진 사용자 지정 경로 테이블을 만들 수 있습니다. hello 읽기 사용자 정의 경로 대 한 자세한 toolearn [사용자 정의 경로](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **경계 게이트웨이 프로토콜 (BGP):** Azure VPN 게이트웨이 또는 express 경로 연결을 사용 하 여 VNet tooyour 온-프레미스 네트워크를 연결 하는 경우 BGP 경로 tooyour Vnet에 전파할 수 있습니다. BGP는 hello 표준 라우팅 프로토콜 hello 인터넷 tooexchange 라우팅과 연결 가능성 정보 두 개 이상의 네트워크 사이에서 일반적으로 사용 합니다. Azure 가상 네트워크를 BGP 사용 hello Azure VPN 게이트웨이 및 온-프레미스 VPN 장치를 사용 하 여 hello 축을 사용 하는 경우 호출된 BGP 피어 또는 인접 한 항목 tooexchange "라우팅합니다" hello 가용성 및 해당 접두사에 대해 두 게이트웨이 알려주는 hello 게이트웨이 또는 라우터로 관련 된 통해 toogo 합니다. BGP 경로 BGP 게이트웨이 한 BGP 피어 tooall에서 학습을 전파 하 여 여러 네트워크 간에 전송 라우팅과 활성화할 수도 다른 BGP 피어입니다. BGP에 대 한 자세한 정보는 toolearn 참조 hello [Azure VPN 게이트웨이 개요를 사용한 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

## <a name="manageability"></a>관리 효율성

Azure는 hello 다음 toomonitor 도구 및 네트워킹 관리를 제공 합니다.
- **작업 로그:** 모든 Azure 리소스 작업 수행에 대 한 정보를 제공 하는 작업 로그에는 작업의 상태를 배치 하 고 hello 작업을 시작한 사람입니다. 활동 로그를 읽을 hello에 대 한 자세한 toolearn [활동 로그 개요](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **진단 로그:** 정기적 감사와 비 정기적인 이벤트 만들고 네트워크 리소스에 의해 및 Azure 저장소 계정에 로그인 tooan Azure 이벤트 허브를 전송 하거나 tooAzure 로그 분석을 전송 합니다. 진단 로그는 리소스의 toohello 상태 정보를 제공합니다. Load Balancer(인터넷 연결), 네트워크 보안 그룹, 경로 및 Application Gateway에서 사용할 수 있습니다. 진단 로그를 읽을 hello에 대 한 자세한 toolearn [진단 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **메트릭:** 메트릭은 리소스에 대해 일정 기간 동안 수집된 성능 측정 및 카운터입니다. 메트릭을 사용 하는 tootrigger 경고 임계값에 따라 될 수 있습니다. 현재 메트릭은 Application Gateway에서 사용할 수 있습니다. hello 읽을 메트릭에 대 한 자세한 toolearn [메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **문제 해결:** 문제 해결 정보는 hello Azure 포털에서 직접 액세스할 수 있습니다. hello 정보 ExpressRoute, VPN 게이트웨이, 응용 프로그램 게이트웨이, 네트워크 보안 로그, 경로, DNS, 부하 분산 장치 및 트래픽 관리자의 일반적인 문제를 진단할 수 있습니다.
- **RBAC(역할 기반 액세스 제어):** RBAC(역할 기반 액세스 제어)를 사용하여 네트워킹 리소스를 만들고 관리할 수 있는 사용자를 제어합니다. 에 대 한 자세한 RBAC hello 읽어 [RBAC 시작](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서. 
- **패킷 캡처:** hello 서비스는 제공 된 Azure 네트워크 감시자 hello hello VM 내에서 확장을 통해 VM에는 패킷 캡처 기능 toorun 합니다. 이 기능은 Linux 및 Windows VM에서 사용할 수 있습니다. 패킷 캡처를 hello 읽기에 대 한 자세한 toolearn [패킷 캡처 개요](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **IP 흐름 확인:** 네트워크 감시자 사용 하면 Azure VM 및 원격 리소스 toodetermine 사이의 tooverify IP 흐름 패킷을 허용 또는 거부 여부. 이 기능은 관리자 hello 기능을 제공 tooquickly 연결 문제를 진단 합니다. tooverify IP 이동 하는 방법에 대 한 자세한 toolearn 읽을 hello [IP 흐름 확인 개요](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **VPN 연결 문제 해결:** hello 네트워크 감시자의 VPN 문제 해결사 기능 연결 또는 게이트웨이 기능 tooquery hello 및 hello 리소스의 hello 상태 확인을 제공 합니다. VPN 연결을 읽기 hello 문제를 해결 하는 방법에 대 한 자세한 toolearn [VPN 연결 문제 해결 개요](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **네트워크 토폴로지 보기:** 네트워크 감시자를 VNet에 hello 네트워크 리소스의 그래픽 표현을 보려면 합니다. 네트워크 토폴로지를 hello 읽는 보기에 대 한 자세한 toolearn [토폴로지 개요](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

## <a name="tools"></a>도구 배포 및 구성

배포 하 고 hello 다음 도구를 사용 하 여 Azure 네트워킹 리소스를 구성할 수 있습니다.

- **Azure Portal:** 브라우저에서 실행되는 그래픽 사용자 인터페이스입니다. 열기 hello [Azure 포털](http://portal.azure.com)합니다.
- **Azure PowerShell:** Windows 컴퓨터에서 Azure를 관리하기 위한 명령줄 도구입니다. Azure PowerShell 하면 자세히 읽는 hello [Azure PowerShell 개요](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **Azure CLI(명령줄 인터페이스):** Linux, macOS 또는 Windows 컴퓨터에서 Azure를 관리하기 위한 명령줄 도구입니다. 읽는 hello 하 여 Azure CLI hello에 대 한 자세한 [Azure CLI 개요](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- **Azure 리소스 관리자 템플릿:** hello 인프라 및 Azure 솔루션의 구성을 정의 하는 JSON 형식의 파일입니다. 템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다. hello 읽을 템플릿을 작성 하는 방법에 대 한 자세한 toolearn [템플릿 만들기에 대 한 유용한](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서. 템플릿은 hello Azure 포털 CLI 또는 PowerShell로 배포할 수 있습니다. hello 중 하나 템플릿으로 지금 바로 시작 tooget hello에 미리 구성 된 템플릿 수를 제공 하는 배포 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/?term=network) 라이브러리입니다. 

## <a name="pricing"></a>가격

일부 hello Azure의 네트워킹 서비스는 충전 있고 나머지는 무료입니다. 보기 hello [가상 네트워크](https://azure.microsoft.com/pricing/details/virtual-network), [VPN 게이트웨이](https://azure.microsoft.com/pricing/details/vpn-gateway), [응용 프로그램 게이트웨이](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [부하 분산 장치](https://azure.microsoft.com/pricing/details/load-balancer), [네트워크 감시자](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [트래픽 관리자](https://azure.microsoft.com/pricing/details/traffic-manager) 및 [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) 가격에 대 한 자세한 내용은 페이지입니다.

## <a name="next-steps"></a>다음 단계

- 첫 번째 VNet을 만들고 몇 가지 Vm tooit hello의 hello 단계를 완료 하 여 연결 [첫 번째 가상 네트워크를 만든](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- Hello의 hello 단계를 완료 하 여 사용자 컴퓨터 tooa VNet 연결 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.
- Hello의 hello 단계를 완료 하 여 인터넷 트래픽을 toopublic 서버의 부하를 분산 [에서 인터넷 연결 부하 분산 장치 만들기](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) 문서.

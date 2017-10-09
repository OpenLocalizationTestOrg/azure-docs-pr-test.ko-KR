---
title: "네트워크 보안 aaaAzure | Microsoft Docs"
description: "다양 한 종류의 계산 인스턴스를 포함 하는 클라우드 기반 컴퓨팅 서비스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스에 알아봅니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure 네트워크 보안

회원님의 보안은 hello 클라우드에서 작업 하나 고 Azure 보안에 대 한 정확 하 고 시기 적절 한 정보를 찾을 얼마나 중요 한지 됩니다. Hello 최상의 이유 toouse Azure 응용 프로그램 및 서비스에 대 한 중 하나에 Azure의 다양 한 보안 도구 및 기능 활용 tootake입니다. 이러한 도구와 기능 hello Azure 플랫폼에서 가능한 toocreate 보안 솔루션을 확인할 수 있습니다.

Microsoft Azure는 고객 데이터의 기밀성, 무결성 및 가용성을 제공하는 한편 투명한 책임도 가능하게 합니다. toohelp 이해 하는 데 hello 컬렉션 hello 고객의 관점에서 Microsoft Azure 내에서 구현 하는 네트워크 보안 제어,이 문서의 "Azure 네트워크 보안" 쓰여집니다 tooprovide hello 네트워크 보안에 대 한 포괄적인 개요 Microsoft Azure와 함께 사용할 수를 제어 합니다.

이 문서는 tooinform hello 광범위 한 네트워크에 대 한 사용자 제어를 Azure의 hello 솔루션을 배포한 tooenhance hello 보안을 구성할 수 것입니다. 관심이 있는 경우 어떤 microsoft에서 않습니다 toosecure hello 네트워크 패브릭의 hello Azure 플랫폼 자체 hello hello Azure 보안 섹션을 참조 하세요 [Microsoft 보안 센터](https://www.microsoft.com/trustcenter/security/azure-security)합니다.

## <a name="azure-platform"></a>Azure 플랫폼

Azure는 다양한 운영 체제, 프로그래밍 언어, 프레임워크, 도구, 데이터베이스 및 장치를 지원하는 공용 클라우드 서비스 플랫폼입니다.  Docker 통합으로 Linux 컨테이너를 실행할 수 있습니다. JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드할 수 있습니다. iOS, Android 및 Windows 장치용 백 엔드를 빌드할 수 있습니다. Azure 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

클라우드 기반의 toomanage hello 보안을 제공 하 고, 사용 하는 조직의 능력 tooprotect 응용 프로그램 및 사용 하 여 데이터 서비스 및 hello 컨트롤 hello, 빌드 또는 공용 클라우드 서비스 공급자에 게 IT 자산을 마이그레이션하는 경우 자산에 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고는 기업의 보안 요구 사항을 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 광범위 한 보안 구성 가능한 옵션 및 hello 기능 toocontrol 컬렉션으로 보안 toomeet hello 조직의 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다.

## <a name="abstract"></a>요약

Microsoft 공용 클라우드 서비스는 대규모 서비스와 인프라, 엔터프라이즈급 기능 및 여러 하이브리드 연결 옵션을 제공합니다. Tooaccess hello 인터넷을 통해 또는 개인 네트워크 연결을 제공 하는 Azure ExpressRoute와 이러한 서비스를 선택할 수 있습니다. Microsoft Azure 플랫폼 hello tooseamlessly 수 있습니다. 다중 계층 아키텍처를 구축 하 고 hello 클라우드로 인프라를 확장 합니다. 또한 타사 보안 서비스 및 가상 어플라이언스를 통해 향상된 기능을 구현할 수 있습니다.

Azure의 네트워크 서비스는 기본적으로 유연성, 가용성, 탄력성, 보안 및 무결성을 최대화합니다. 이 백서는 Azure의 hello 네트워킹 기능에 대 한 자세한 내용 및 고객이 Azure의 기본 보안 기능 toohelp를 사용 하는 방법을 정보의 정보 자산을 보호를 제공 합니다.

hello를 위한 것이 백서에 대 한 대상 그룹 포함:

- Azure에서 사용 가능하고 지원되는 보안 솔루션을 찾고 있는 기술 관리자, 네트워크 관리자 및 개발자

-   Sme 또는 높은 수준의 개요를 tooget 하려는 프로세스 경영진 hello Azure 네트워킹 기술 및 논의 hello Azure 공용 클라우드에서에서 네트워크 보안에 관련 된 서비스입니다.

## <a name="azure-networking-big-picture"></a>Azure 네트워킹의 전반적 이해
Microsoft Azure 응용 프로그램 및 서비스 연결 요구 사항 강력한 네트워킹 인프라 toosupport를 포함합니다. Azure 호스팅 리소스 및 hello 인터넷에서에서 tooand 및 Azure 있으며 온-프레미스 간에 Azure에 배치 된 리소스 간에 네트워크 연결 됩니다.

![Azure 네트워킹의 전반적 이해](media/azure-network-security/azure-network-security-fig-1.png)

hello [Azure 네트워크 인프라](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) toosecurely 하면 가상 네트워크 (Vnet)를 사용 하 여 다른 Azure 리소스 tooeach를 연결 하는 사용 하도록 설정 합니다. VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet는 hello Azure 클라우드 전용 네트워크 tooyour 구독의 논리적 격리입니다. Vnet tooyour 온-프레미스 네트워크를 연결할 수 있습니다.

Azure 지원 WAN 링크 연결 tooyour 온-프레미스 네트워크와 Azure 가상 네트워크와 전용 [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)합니다. hello를 통해 전달 되지 않는 전용된 연결을 사용 하 여 사이트와 Azure 간의 hello 링크 공용 인터넷 합니다. Azure 응용 프로그램에서 여러 데이터 센터를 실행 하는 경우 사용할 수 있습니다 [Azure 트래픽 관리자](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute 사용자의 요청을 hello 응용 프로그램의 인스턴스를 통해 자동으로 조정 합니다. 또한 트래픽 tooservices hello 인터넷에서에서 액세스할 수 있는 경우 Azure에서 실행 중이지 라우팅할 수 있습니다.

## <a name="enterprise-view-of-azure-networking-components"></a>Azure 네트워킹 구성 요소의 엔터프라이즈 보기
Azure는 많은 네트워킹 구성 요소 관련 toonetwork 보안 논의 합니다. 이러한 네트워킹 구성 요소에서 설명 하지 않으며 hello 보안에 집중 관련된 toothem 합니다.

> [!Note]
> Azure 네트워킹의 일부 측면은 설명 – 논의 항목만 toobe 계획 하 고 서비스 및 Azure에서 배포 응용 프로그램 보안 네트워크 인프라 디자인에 중요으로 간주 합니다.

이 문서에서는 이후 표시 되 커버 hello Azure 네트워킹 엔터프라이즈 기능:

-   기본 네트워크 연결

-   하이브리드 연결

-   Single Sign On 설정

-   네트워크 유효성 검사

### <a name="basic-network-connectivity"></a>기본 네트워크 연결

hello [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) toosecurely 하면 가상 네트워크 (VNet)를 사용 하 여 다른 Azure 리소스 tooeach를 연결 하는 서비스 수 있습니다. VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet는 hello Azure 네트워크 인프라 전용 tooyour 구독의 논리적 격리입니다. 다른 Vnet tooeach을 연결할 수 있습니다 및 tooyour 온-프레미스 사이트 간 Vpn을 사용 하 여 네트워크와 전용 [WAN 링크](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)합니다.

![기본 네트워크 연결](media/azure-network-security/azure-network-security-fig-2.png)

Hello Vm toohost 서버 사용 하 여 Azure에서 이해로 hello 질문 해당 Vm tooa 네트워크를 연결 하는 방법입니다. hello 대답은 Vm을 tooan 연결 [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)합니다.

Azure 가상 네트워크는 hello 가상 네트워크와 같은 온-프레미스 Microsoft Hyper-v 또는 VMware 같은 고유한 가상화 플랫폼 솔루션을 사용 합니다.

#### <a name="intra-vnet-connectivity"></a>VNet 내 연결

다른 Vnet tooeach 연결할 수 있습니다, Vnet에 걸쳐 서로 tooeither VNet toocommunicate 연결 리소스를 사용 하도록 설정 합니다. Hello 옵션 tooconnect Vnet tooeach 다른 다음 중 하나 또는 모두를 사용할 수 있습니다.

- **피어 링:** 사용 리소스 연결 hello 내에서 Azure Vnet toodifferent 서로 동일한 Azure 위치 toocommunicate 합니다. hello 대역폭 및 대기 시간 VNet이 hello 간에 hello 동일 하면 hello 리소스에 연결 된 toohello 것 처럼 동일한 VNet입니다. 피어 링을 대 한 자세한 toolearn 읽을 [가상 네트워크 피어 링](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)합니다.

 ![피어링](media/azure-network-security/azure-network-security-fig-3.png)

- **VNet 대 VNet 연결:** 사용 리소스 연결 hello 내에서 Azure VNet toodifferent 같거나 다른 Azure 위치입니다. 피어링과 달리, 트래픽이 Azure VPN Gateway를 통과해야 하기 때문에 VNet 간에 대역폭이 제한됩니다.

![VNet 간 연결](media/azure-network-security/azure-network-security-fig-4.png)


Vnet hello 읽을 VNet 대 VNet 연결을 통해 연결 하는 방법에 대 한 자세한 toolearn [VNet 대 VNet 연결 문서를 구성](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.

#### <a name="azure-virtual-network-capabilities"></a>Azure Virtual Network 기능:

볼 수 있듯이 tooother 네트워크 리소스에 보안 방식으로 연결할 수 있도록 Azure 가상 네트워크 가상 컴퓨터 tooconnect toohello 네트워크를 제공 합니다. 그러나 기본 연결 정당한 hello 시작입니다. hello hello Azure 가상 네트워크 서비스의 다음 기능을 노출 hello Azure 가상 네트워크의 보안 특성:

-   격리

-   인터넷 연결

-   Azure 리소스 연결

-   VNet 연결

-   온-프레미스 연결

-   트래픽 필터링

-   라우팅

**격리**

VNet은 서로 완전히 [격리](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)됩니다. 개발, 테스트 및 프로덕션 사용 하 여 동일한을 hello에 대 한 별도 Vnet을 만들 수 있습니다 [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) 오류를 해결 합니다. 반대로, 여러 CIDR 주소 블록을 사용하는 VNet을 만들어 네트워크를 서로 연결할 수도 있습니다. VNet은 여러 서브넷으로 분할할 수 있습니다.

Azure Vm에 대 한 내부 이름 확인을 제공 하 고 [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) 역할 인스턴스가 tooa VNet를 연결 합니다. 필요에 따라 VNet toouse Azure 내부 이름 확인을 사용 하는 대신 고유한 DNS 서버를 구성할 수 있습니다.

각 Azure [구독](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) 및 Azure [지역](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) 내에서 여러 VNet을 구현할 수 있습니다. 각 VNet은 다른 VNet에서 격리됩니다. 각 VNet에 대해 다음을 수행할 수 있습니다.

-   공용 및 사설(RFC 1918) 주소를 사용하여 사용자 지정 사설 IP 주소 공간을 지정합니다. Azure 리소스 연결된 toohello VNet 개인 IP 주소 할당 hello 주소 공간에서 할당 합니다.

-   Hello VNet 주소 공간 tooeach 서브넷의 일부를 할당 하 고 hello VNet 하나 이상의 서브넷으로 분할 합니다.

-   Azure 제공 이름 확인을 사용 하거나 tooa VNet를 연결 하는 리소스에서 사용 하기 위해 자체 DNS 서버 지정 합니다. hello 읽을 Vnet에서 이름 확인에 대 한 자세한 toolearn [Vm 및 클라우드 서비스에 대 한 이름 확인](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances)합니다.

**인터넷 연결**

모든 [Azure 가상 컴퓨터 (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) 및 연결 된 VNet tooa가 클라우드 서비스 역할 인스턴스 기본적으로 toohello 인터넷에 액세스 합니다. 필요에 따라 toospecific 리소스에 인바운드 액세스를 설정할 수도 있습니다. (VM) 및 연결 된 VNet tooa가 클라우드 서비스 역할 인스턴스 기본적으로 toohello 인터넷에 액세스 합니다. 필요에 따라 toospecific 리소스에 인바운드 액세스를 설정할 수도 있습니다.

모든 리소스 연결된 tooa VNet 기본적으로 인터넷 아웃 바운드 연결 toohello가 있어야 합니다. hello hello 리소스의 개인 IP 주소는 원본 네트워크 주소 hello Azure 인프라에 의해 (SNAT) tooa 공용 IP 주소를 변환 합니다. 사용자 지정 라우팅 및 트래픽 필터링을 구현 하 여 hello 기본 연결을 변경할 수 있습니다. hello 읽을 아웃 바운드 인터넷 연결에 대 한 자세한 toolearn [Azure의 아웃 바운드 연결 이해](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.

toocommunicate 인바운드 tooAzure 리소스에서 인터넷을 hello 또는 toocommunicate 아웃 바운드 toohello SNAT, 리소스 없이 인터넷에 공용 IP 주소를 할당 해야 합니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [공용 IP 주소](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address)합니다.

**Azure 리소스 연결**

[Azure 리소스](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 클라우드 서비스 및 Vm에 연결 된 toohello 수와 같은 동일한 VNet입니다. hello 리소스 다른 tooeach 연결할 수 있는 개인 IP를 사용 하 여 주소, 서브넷이 서로 다른 경우에 합니다. Azure 없습니다 tooconfigure 하 고 경로 관리 하므로 기본 서브넷, Vnet 및 온-프레미스 네트워크 간의 라우팅을 제공 합니다.

여러 Azure 리소스 tooa 가상 컴퓨터 (VM), 클라우드 서비스, 앱 서비스 환경 및 가상 컴퓨터 크기 집합 같이 VNet을 연결할 수 있습니다. Vm은 네트워크 인터페이스 (NIC)를 통해 VNet 내의 서브넷 tooa를 연결합니다. hello 읽을 Nic에 대 한 자세한 toolearn [네트워크 인터페이스](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface)합니다.

**VNet 연결**

[Vnet](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 수 있으며 연결 된 tooeach 다른, tooany VNet toocommunicate 다른 VNet에 리소스와 연결 된 리소스를 사용 하도록 설정 합니다.

다른 Vnet tooeach 연결할 수 있습니다, Vnet에 걸쳐 서로 tooeither VNet toocommunicate 연결 리소스를 사용 하도록 설정 합니다. Hello 옵션 tooconnect Vnet tooeach 다른 다음 중 하나 또는 모두를 사용할 수 있습니다.

- **피어 링:** 사용 리소스 연결 hello 내에서 Azure Vnet toodifferent 서로 동일한 Azure 위치 toocommunicate 합니다. hello Vnet hello 리소스 toohello 연결 된 경우와 동일 hello는 hello에서 대기 시간 및 대역폭을 피어 링에 대 한 동일한 VNet.toolearn 읽기 hello [가상 네트워크 피어 링](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)합니다.

- **VNet 대 VNet 연결:** 사용 리소스 연결 hello 내에서 Azure VNet toodifferent 같거나 다른 Azure 위치입니다. 피어링과 달리, 트래픽이 Azure VPN Gateway를 통과해야 하기 때문에 VNet 간에 대역폭이 제한됩니다. VNet 대 VNet 연결을 사용 하 여 Vnet를 연결 하는 방법에 대 한 자세한 toolearn 합니다. toolearn hello를 더 읽기 [VNet 대 VNet 연결 구성](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) 합니다.

**온-프레미스 연결**

Vnet을 너무 연결 될 수 있습니다.[온-프레미스](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 네트워크와 Azure 간의 개인 네트워크 연결을 통해 또는 hello 인터넷을 통해 사이트 간 VPN 연결을 통해 네트워크입니다.

온-프레미스 네트워크 tooa hello 다음 옵션을 조합 하 여 VNet을 연결할 수 있습니다.

- **지점 및 사이트 간 가상 사설망 (VPN):** 간에 단일 PC tooyour 연결 된 네트워크 및 VNet hello를 설정 합니다. 이 연결 유형에 거의 또는 전혀 변경 tooyour 기존 네트워크 필요 하기 때문에 수행 하는 개발자를 위한 또는 azure를 하는 경우 유용 합니다. hello 연결 hello PC와 hello VNet 간의 인터넷 hello 통한 hello SSTP 프로토콜 암호화 tooprovide 통신을 사용합니다. hello 트래픽이 hello 인터넷에서 이동 하는 지점-사이트 VPN에 대 한 hello 대기 시간은 예측 가능한 하지 않습니다.

- **사이트 간 VPN:** VPN 장치와 Azure VPN Gateway 간에 설정됩니다. 이 연결 유형에 모든 온-프레미스 리소스를 tooaccess VNet 권한을 부여할 수 있습니다. hello 연결은 온-프레미스 장치와 hello Azure VPN 게이트웨이 hello 인터넷을 통해 암호화 된 통신을 제공 하는 IPsec/IKE VPN입니다. hello 트래픽이 트래버스하 hello 인터넷 사이트와 사이트 간 연결에 대 한 대기 시간 hello은 예측 가능한 하지 않습니다.

- **Azure ExpressRoute:** ExpressRoute 파트너를 통해 네트워크와 Azure 간에 설정됩니다. 이 연결은 사설 전용입니다. 트래픽 hello 인터넷을 통과 하지 않는 합니다. ExpressRoute 연결에 대 한 hello 대기 시간 예측할 수 없으므로 트래픽 hello 인터넷을 트래버스 하지 않습니다. 모든 hello 이전 연결 옵션을 hello 읽기에 대 한 자세한 toolearn [연결 토폴로지 다이어그램](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.

**트래픽 필터링**

VM 및 Cloud Services 역할 인스턴스 [네트워크 트래픽](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)을 원본 IP 주소 및 포트, 대상 IP 주소 및 포트 및 프로토콜별로 인바운드 및 아웃바운드에 따라 필터링할 수 있습니다.

Hello 다음 옵션 중 하나 또는 모두를 사용 하 여 서브넷 간의 네트워크 트래픽을 필터링 할 수 있습니다.

- **네트워크 보안 그룹 (NSG):** 각 NSG에는 원본 및 대상 IP 주소, 포트 및 프로토콜 toofilter 트래픽 수 있도록 하는 여러 개의 인바운드 및 아웃 바운드 보안 규칙 포함 될 수 있습니다. NSG tooeach VM에서 NIC에 적용할 수 있습니다. 다른 Azure 리소스에 연결 되어 또는 NIC에 NSG toohello 서브넷도 적용할 수 있습니다. hello 읽을 Nsg에 대 한 자세한 toolearn [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)합니다.

- **Virtual Network 어플라이언스:** Virtual Network 어플라이언스는 방화벽과 같은 네트워크 기능을 수행하는 소프트웨어를 실행하는 VM입니다. Hello Azure Marketplace에서에서 사용 가능한 NVAs의 목록을 봅니다. WAN 최적화 및 기타 네트워크 트래픽 기능을 제공하는 NVA도 사용할 수 있습니다. NVA는 일반적으로 사용자 정의 경로 또는 BGP 경로와 함께 사용됩니다. 또한 Vnet 간의 NVA toofilter 트래픽을 사용할 수 있습니다.

**라우팅**

자체 경로를 구성하여 또는 네트워크 게이트웨이 통해 BGP 경로를 사용하여 Azure의 기본 라우팅을 선택적으로 재정의할 수 있습니다.

Azure에서는 기본적으로, 모든 VNet toocommunicate에서 리소스 연결 된 tooany 서브넷을 사용할 수 있는 경로 테이블을 만듭니다. 구현할 수 있습니다 또는 둘 다의 hello 옵션 toooverride 다음 hello Azure 만듭니다 기본 경로:

- **사용자 정의 경로:** 각 서브넷 트래픽이 라우팅된 toofor가 제어 하는 경로 가진 사용자 지정 경로 테이블을 만들 수 있습니다. 사용자 정의 경로 hello 읽기에 대 한 자세한 toolearn [사용자 정의 경로](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)합니다.

- **BGP 경로:** Azure VPN 게이트웨이 또는 express 경로 연결을 사용 하 여 VNet tooyour 온-프레미스 네트워크를 연결 하는 경우 BGP 경로 tooyour Vnet에 전파할 수 있습니다.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>하이브리드 인터넷 연결: tooan 온-프레미스 네트워크에 연결
온-프레미스 네트워크 tooa hello 다음 옵션을 조합 하 여 VNet을 연결할 수 있습니다.

-   인터넷 연결

-   P2S VPN(지점-사이트 간 VPN)

-   S2S VPN(사이트 간 VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>인터넷 연결

해당 이름에서 알 수 있듯이 인터넷 연결 사용 하면 작업 hello 인터넷에서에서 액세스할 수 있는 함으로써 hello 가상 네트워크 내에 존재 하는 다른 공용 끝점 tooworkloads 노출할 수 있습니다. 사용 하 여 이러한 작업을 노출 될 수 있습니다 [인터넷 연결 부하 분산 장치](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) 또는 VM toohello 주소는 공용 IP를 할당 하면 됩니다. 이러한 방식으로 막대로 가능한 모든 호스트 방화벽 제공 해당 가상 컴퓨터에 hello 인터넷 toobe 수 tooreach [네트워크 보안 그룹 (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), 및 [사용자 정의 경로](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) 허용 하는 toohappen 합니다.

이 시나리오에서는 수 없습니다 toobe 공용 toohello 인터넷 필요한 응용 프로그램에 노출 하 고 어디에서 든 지 또는 작업의 hello 구성에 따라 특정 위치에서 수 tooconnect tooit 수 있습니다.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>지점 및 사이트 간 VPN 또는 사이트 간 VPN
이러한 두 위치에 동일한 범주를 hello 합니다. 프로그램 VNet toohave VPN 게이트웨이 필요 모두 있으며 tooit 워크스테이션에 대 한 VPN 클라이언트를 사용 하 여 hello의 일환으로 연결할 수 있습니다 [지점-사이트 구성](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 온-프레미스를 구성할 수 있습니다 또는 [VPN장치](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe 수 tooterminate 사이트 간 VPN. 이러한 방식으로 온-프레미스 장치 tooresources hello VNet 내에서 연결할 수 있습니다.

지점 및 사이트 간 (P2S) 구성에는 개별 클라이언트 컴퓨터 tooa 가상 네트워크에서 보안 연결을 만들 수 있습니다. P2S는 SSTP를 통한 VPN 연결입니다(보안 소켓 터널링 프로토콜).

![지점 및 사이트 간 VPN](media/azure-network-security/azure-network-security-fig-5.png)

지점 및 사이트 연결은 가정 이나 회의 센터에서와 같은 tooconnect tooyour 원격 위치에서 VNet을 원하는 또는 tooconnect tooa 가상 네트워크를 필요로 하는 몇 가지 클라이언트에만 있는 경우에 유용 합니다.

P2S 연결에는 VPN 장치 또는 공용 IP 주소가 필요하지 않습니다. Hello 클라이언트 컴퓨터에서 VPN 연결 hello를 설정 합니다. 따라서 P2S 많은 온-프레미스 장치 및 컴퓨터 tooyour Azure 네트워크에서 영구 연결 해야 할 경우 tooconnect tooAzure 방법은 권장 되지 않습니다.

![사이트 간 VPN](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> 지점 및 사이트 간 연결에 대 한 자세한 내용은 참조 hello [지점 및 사이트 간 FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal)합니다.

사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다.

이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다. 이 연결이 이루어집니다 인터넷 hello를 사용 하면 너무 "터널"은 암호화 된 연결 하면 네트워크와 Azure 내에서 정보 계속 합니다. 사이트 간 VPN은 수십 년 동안 모든 규모의 기업에서 배포해 온 안전하고 완성도 높은 기술입니다. 터널 암호화는 [IPsec 터널 모드](https://technet.microsoft.com/library/cc786385.aspx)를 사용하여 수행됩니다.

사이트 간 VPN은 안정적이 고 설정 된 신뢰할 수 있는 기술, hello 터널 내의 트래픽을 인터넷 hello를 트래버스하여 합니다. 또한 대역폭은 상대적으로 제한 된 tooa 최대 약 200 Mbps입니다.

크로스-프레미스 연결에 강력한 보안 또는 성능 수준이 필요한 경우 크로스-프레미스 연결에 Azure ExpressRoute를 사용하는 것이 좋습니다. ExpressRoute는 온-프레미스 위치 또는 Exchange 호스팅 공급자 사이의 WAN 링크입니다. Telco 연결 이므로 데이터 hello 인터넷을 통해 전송 하지 않습니다 이며 노출된 되지 toohello 인터넷 통신에 내재 된 잠재적 위험 합니다.

> [!Note]
> VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways)를 참조하세요.

#### <a name="dedicated-wan-link"></a>전용 WAN 링크
Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 통해 지원 되는 전용된 개인 연결을 통해 Azure hello로 온-프레미스 네트워크를 확장할 수 있습니다.

ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해.

![ 전용 WAN 링크](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> 방법에 대 한 내용은 tooconnect ExpressRoute를 사용 하 여 네트워크 tooMicrosoft 참조 [ExpressRoute 연결 모델](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) 및 [express 경로 기술 개요](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)합니다.

으로 hello 사이트 간 VPN 옵션과 ExpressRoute 수도 있습니다 반드시 하나의 VNet에 없는 tooconnect tooresources를. 사실, SKU hello에 따라 too10 Vnet을 연결할 수 있습니다. Hello 있는 경우 [premium 추가 기능](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), 연결 tooup too100 Vnet 대역폭에 따라 수 있습니다. 어떤 이러한 유형의 연결 모양 좋은지, 읽기에 대 한 자세한 toolearn [연결 토폴로지 다이어그램](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.

### <a name="security-controls"></a>보안 컨트롤
Azure Virtual Network는 다른 가상 네트워크와 분리되고 온-프레미스 네트워크에서 사용하는 많은 보안 컨트롤을 지원하는 안전한 논리적 네트워크를 제공합니다. 고객 자체의 구조를 사용 하 여 만들: 서브넷-자신의 개인 IP 주소 범위를 사용 하 여, 경로 테이블을 구성, 네트워크 보안 그룹은 액세스 제어 목록 (Acl), 게이트웨이 및 가상 어플라이언스 toorun hello 클라우드에서 작업량입니다.

hello 다음은 보안 제어를 통해 Azure 가상 네트워크에 사용할 수 있습니다.

-   네트워크 액세스 컨트롤

-   사용자 정의 경로

-   네트워크 보안 어플라이언스

-   Application Gateway

-   Azure 웹 응용 프로그램 방화벽

-   네트워크 가용성 컨트롤

#### <a name="network-access-controls"></a>네트워크 액세스 컨트롤
Hello Azure 가상 네트워크 (VNet)은 Azure 네트워킹 모델의 hello 토대 하 격리 및 보안을 제공 하는 동안 hello [보안 그룹 NSG (네트워크)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) 은 네트워크 트래픽을 tooenforce 및 제어를 사용 하는 hello 주 도구 hello 네트워크 수준에서 규칙입니다.

![ 네트워크 액세스 컨트롤](media/azure-network-security/azure-network-security-fig-8.png)


직접 인터넷 통신 또는 허용 또는 거부 크로스-프레미스 연결을 통해 고객의 네트워크의 시스템에서 가상 네트워크 내에서 hello 작업 간의 통신 하면 액세스를 제어할 수 있습니다.

Hello 다이어그램 Vnet 및 Nsg를 모두 Nsg, UDR, 및 네트워크 가상 어플라이언스 hello 보호 네트워크 toocreate 사용 되는 보안 경계 tooprotect hello 응용 프로그램 배포를 될 수 있는 hello Azure 전반적인 보안 스택에서 특정 계층에 있어야 합니다.

Nsg 5-튜플 tooevaluate 트래픽을 사용 (하 고 hello NSG에 대 한 hello 규칙 구성에 사용 되):

-   [원본 및 대상 IP 주소](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [원본 및 대상 포트](https://technet.microsoft.com/library/dd197515)

-   프로토콜: [TCP(Transmission Control Protocol)](https://technet.microsoft.com/library/cc940037.aspx) 또는 [UDP(User Datagram Protocol)](https://technet.microsoft.com/library/cc940034.aspx)

즉, 단일 VM와 그룹 간의 액세스를 제어할 수 있습니다, Vm 또는 단일 VM tooanother의 VM을 단일 또는 전체 서브넷 간의 합니다. 또한 전체 패킷 검사가 아닌 간단한 상태 저장 패킷 필터링이 사용됩니다. 네트워크 보안 그룹에는 프로토콜 유효성 검사나 네트워크 수준 IDS 또는 IPS 기능이 없습니다.

NSG는 알고 있어야 하는 몇 가지 기본 제공 규칙을 제공합니다. 다음과 같습니다.

-   **특정 가상 네트워크 내에서 모든 트래픽을 허용:** hello에 있는 모든 Vm 동일한 Azure 가상 네트워크는 서로 통신할 수 있습니다.

-   **Azure 부하 분산 tooinbound 허용:** 이 규칙 hello Azure 부하 분산 장치에 대 한 모든 소스 주소 tooany 대상 주소에서의 트래픽을 허용 합니다.

-   **모든 인바운드 거부:** 이 규칙은 안녕하세요 명시적으로 허용 된 인터넷에서에서 소싱 하는 모든 트래픽을 차단 합니다.

-   **모든 트래픽 아웃 바운드 toohello 인터넷 허용:** 이 규칙은 Vm tooinitiate 연결 toohello 인터넷 허용 합니다. 이러한 연결을 시작 하지 않으려면 규칙 tooblock toocreate 하는 연결 또는 강제 터널링을 적용 합니다.

#### <a name="system-routes-and-user-defined-routes"></a>시스템 경로 및 사용자 정의 경로

Azure에서 가상 컴퓨터 (Vm) tooa 가상 네트워크 (VNet)를 추가할 때 hello Vm은 서로 수 toocommunicate hello 네트워크를 통해 자동으로 확인할 수 있습니다. Hello Vm 서브넷이 서로 다른 경우에 게이트웨이 toospecify를 않아도 됩니다.

hello 같은 기준이 hello Vm toohello에서 통신에 대 한 공용 인터넷 및 tooyour Azure에서 하이브리드 연결 데이터 센터를 사용할 수 있는지를 소유 하는 경우에 tooyour 온-프레미스 네트워크입니다.

![시스템 경로](media/azure-network-security/azure-network-security-fig-9.png)

통신의이 흐름은 Azure 일련의 시스템 경로 toodefine IP 트래픽이 흐르는 방법을 사용 하기 때문에 가능 합니다. Hello 흐름 hello 다음 시나리오에서에서이 통신을 제어 하는 시스템 경로:

-   내에서 동일한 서브넷을 hello 합니다.

-   VNet 내의 서브넷 tooanother에서.

-   Vm toohello 인터넷 합니다.

-   VPN 게이트웨이 통해는 VNet tooanother VNet입니다.

-   VNet tooanother VNet 피어 링을 통해 VNet에서에서 ([서비스 체인](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   VPN 게이트웨이 통해 VNet tooyour 온-프레미스 네트워크입니다.

모든 네트워크 패킷 tooenforce 특정의 온-프레미스 검사 해야 하는 규정 준수 요구 사항의 정책 및 대부분의 기업에서는 엄격한 보안이 있습니다. 호출 하는 메커니즘을 제공 하는 azure [강제 터널링](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) 사용자 지정 경로 만들거나 여 hello tooon-프레미스 Vm에서에서 트래픽을 라우팅하는 [프로토콜 BGP (경계 게이트웨이)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) 를 통해 광고 Express 경로 또는 VPN입니다.

Azure에서 강제 터널링은 가상 네트워크 UDR(사용자 정의 경로)을 통해 구성됩니다. 트래픽 tooan 리디렉션 온-프레미스 사이트는 기본 경로 toohello Azure VPN 게이트웨이로 표시 됩니다.

hello 다음 섹션에는 Azure 가상 네트워크에 대 한 경로 및 hello 라우팅 테이블의 한 hello 현재 제한:

-   각 가상 네트워크 서브넷에는 기본 제공 시스템 라우팅 테이블이 있습니다. hello 시스템에 대 한 라우팅 테이블에는 3 개의 그룹의 경로 따라 hello에 있습니다.

 -  **지역 VNet 경로:** 직접 toohello의에서 대상 Vm hello 동일한 가상 네트워크

 - **온-프레미스 경로:** toohello Azure VPN 게이트웨이

 -  **기본 경로:** toohello 인터넷 직접 합니다. 패킷을 toohello 개인 IP 주소 hello 이전 두 경로에서 포함 하지 않는 삭제 됩니다.

-   사용자 정의 경로의 hello 릴리스로 라우팅 테이블 tooadd 기본 경로 만들 수 있으며 hello 라우팅 테이블 tooyour VNet 서브넷 tooenable 강제 터널링 이러한 서브넷에 연결 하 여 키를 누릅니다.

-   Hello 크로스-프레미스 로컬 사이트 toohello 연결 된 가상 네트워크 간에 tooset "기본 사이트" 해야합니다.

-   강제 터널링은 동적 라우팅 VPN Gateway(정적 게이트웨이 아님)가 있는 VNet에 연결되어야 합니다.

- Express 경로 강제 터널링이 메커니즘을 통해 구성 되지 않은 하지만 대신 hello ExpressRoute BGP를 통해 기본 경로으로 활성화 되어 피어 링 세션입니다.

> [!Note]
> 자세한 내용은 참조 hello [express 경로 설명서](https://azure.microsoft.com/documentation/services/expressroute/) 자세한 정보에 대 한 합니다.

#### <a name="network-security-appliances"></a>네트워크 보안 어플라이언스
네트워크 보안 그룹 및 사용자 정의 경로 제공할 수는 어느 정도의 hello에서 네트워크 보안 네트워크 및 전송 계층의 hello 동안 [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 원하는 또는 tooenable 필요 toobe 상황 것 이며 네트워킹 스택 hello 상위 수준의 보안입니다. 이러한 상황에서는 Azure 파트너가 제공하는 가상 네트워크 보안 어플라이언스를 배포하는 것이 좋습니다.

![네트워크 보안 어플라이언스](./media/azure-network-security/azure-network-security-fig-10.png)

Azure 네트워크 보안 어플라이언스 VNet 보안 및 네트워크 기능을 개선 하 고 hello 통해 다양 한 공급 업체에서 제공 하는 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com)합니다. 이러한 가상 보안 어플라이언스 tooprovide 배포 될 수 있습니다.

-   고가용성 방화벽

-   침입 방지

-   침입 탐지

-   WAF(웹 응용 프로그램 방화벽)

-   WAN 최적화

-   라우팅

-   부하 분산

-   VPN

-   인증서 관리

-   Active Directory

-   Multi-Factor Authentication

#### <a name="application-gateway"></a>프런트 엔드

[Microsoft Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하는 전용 가상 어플라이언스입니다.

 ![응용 프로그램 게이트웨이](./media/azure-network-security/azure-network-security-fig-11.png)

응용 프로그램 게이트웨이 사용 하면 toooptimize 웹 팜 성능 및 가용성 CPU 집약적인 SSL 종료 toohello 응용 프로그램 게이트웨이 (SSL 오프 로딩)를 오프 로드 합니다. 또한 다음을 비롯한 기타 계층 7 라우팅 기능도 제공합니다.

-   들어오는 트래픽의 라운드 로빈 배포

-   쿠키 기반 세션 선호도

-   URL 경로 기반 라우팅

-   기능 toohost 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트


A [웹 응용 프로그램 방화벽 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) hello 응용 프로그램 게이트웨이의 일부분으로도 제공 됩니다. 일반적인 웹 취약점을 악용 tooweb 응용 프로그램 보호 제공합니다. Application Gateway는 인터넷 연결 게이트웨이, 내부 전용 게이트웨이 또는 둘의 조합으로 구성할 수 있습니다.

Application Gateway WAF는 탐지 또는 방지 모드에서 실행할 수 있습니다. 일반적인 사용 사례는의 악의적인 패턴에 대 한 검색 모드 tooobserve 트래픽 관리자 toorun입니다. 악용 가능성이 감지 되 면 켜는 tooprevention 모드 의심 스러운 들어오는 트래픽을 차단 합니다.

 ![응용 프로그램 게이트웨이](./media/azure-network-security/azure-network-security-fig-12.png)

또한 응용 프로그램 게이트웨이 WAF 수와 통합 되어 실시간 WAF 로그를 사용 하 여 공격 으로부터 웹 응용 프로그램을 모니터링 하는 데 [Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) 및 [Azure 보안 센터](https://azure.microsoft.com/services/security-center/) tootrack WAF 경고 고 쉽게 추세를 모니터링 합니다.

hello JSON 형식이 지정 된 로그가 toohello 고객 저장소 계정 직접 이동합니다. 이러한 로그를 완전히 제어하고 자체 보존 정책을 적용할 수 있습니다.

[Azure 로그 통합](https://aka.ms/AzLog)을 사용하여 이러한 로그를 분석 시스템으로 수집할 수도 있습니다. WAF 로그와도 통합 되어 [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) OMS 로그 분석을 사용할 수 있도록 tooexecute 세분화 된 쿼리는 정교한 합니다.

#### <a name="azure-web-application-firewall-waf"></a>Azure WAF(웹 응용 프로그램 방화벽)

웹 응용 프로그램은 SQL 삽입, 교차 사이트 스크립팅 공격 hello에 나타나는 다른 공격 등의 일반적인 알려진된 취약점을 악용 하는 악의적인 공격의 대상 점점 더 [OWASP 상위 10 개의](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)합니다. 엄격한 유지 관리, 패치 및 hello 응용 프로그램 토폴로지의 여러 계층에서 모니터링 해야 hello 응용 프로그램에서 이러한 악용을 방지 합니다.

 ![Azure WAF(웹 응용 프로그램 방화벽)](./media/azure-network-security/azure-network-security-fig-13.png)

중앙 집중식 [WAF(웹 응용 프로그램 방화벽)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)는 응용 프로그램을 변경할 필요 없이 웹 공격으로부터 보호하고 보안 관리를 간소화합니다.

WAF 솔루션와 각각의 개별 웹 응용 프로그램 보안을 중앙 위치에서 알려진된 취약점의 패치를 적용 하 여 tooa 보안 위협이 더 빠르게 반응 수 있습니다. 기존 응용 프로그램 게이트웨이 변환 된 tooa 웹 응용 프로그램 방화벽을 사용 응용 프로그램 게이트웨이 쉽게 될 수 있습니다.

#### <a name="network-availability-controls"></a>네트워크 가용성 컨트롤

Microsoft Azure를 사용 하 여 다양 한 옵션 toodistribute 네트워크 트래픽이 있습니다. 이러한 옵션은 서로 다르게 작동하며 다른 기능 모음을 포함하고 다양한 시나리오를 지원합니다. 각각을 따로 사용하거나 조합해서 사용할 수 있습니다.

다음은 네트워크 가용성 제어 hello 됩니다.

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Azure Load Balancer**

높은 가용성 및 네트워크 성능을 tooyour 응용 프로그램을 제공합니다. 이 장치는 부하 분산 장치 집합에 정의된 서비스의 정상 인스턴스 간에 들어오는 트래픽을 분산하는 계층 4(TCP, UDP) 부하 분산 장치입니다.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer를 다음과 같이 구성할 수 있습니다.

-   부하 분산 들어오는 인터넷 트래픽을 toovirtual 컴퓨터. 이 구성을 [인터넷 연결 부하 분산](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)이라고 합니다.

-   가상 네트워크의 가상 컴퓨터 간, 클라우드 서비스의 가상 컴퓨터 간 또는 크로스-프레미스 가상 네트워크의 온-프레미스 컴퓨터와 가상 컴퓨터 간에 트래픽을 부하 분산합니다. 이 구성을 [내부 부하 분산](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)이라고 합.

-   외부 트래픽이 tooa 특정 가상 컴퓨터를 전달 합니다.

Hello 클라우드의 모든 리소스 hello 인터넷에서에서 연결할 수 있는 공용 IP 주소 toobe가 필요합니다. Azure의 hello 클라우드 인프라는 해당 리소스에 대 한 라우팅할 수 없는 IP 주소를 사용합니다. Azure 공용 IP 주소 toocommunicate toohello 인터넷 인 네트워크 주소 변환 (NAT)를 사용합니다.

 **Application Gateway**

 응용 프로그램 게이트웨이 hello 응용 프로그램 계층 (hello OSI 네트워크 참조 스택의 계층 7)에서 작동합니다. Hello 클라이언트 연결을 종료 하는 역방향 프록시 서비스로 작동 하 고 전달 tooback 간 끝점을 요청 합니다.

 **Traffic Manager**

Microsoft Azure 트래픽 관리자 다른 데이터 센터에서 서비스 끝점에 대 한 사용자 트래픽의 toocontrol hello 배포를 사용 합니다. Traffic Manager에서 지원되는 서비스 끝점은 Azure VM, Web Apps 및 클라우드 서비스를 포함합니다. 또한 외부, Azure가 아닌 끝점으로 Traffic Manager를 사용할 수 있습니다.

트래픽 관리자 사용 하 여 DNS 도메인 이름 () toodirect 클라이언트 요청에 따라 toohello 가장 적합 한 끝점 hello는 [트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) 및 hello 끝점의 hello 상태입니다. 트래픽 관리자는 트래픽 라우팅 방법 toosuit 다른 응용 프로그램 요구 끝점 상태 다양 한 제공 [모니터링](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring), 및 자동 장애 조치 합니다. 트래픽 관리자는 전체 Azure 지역의 hello 못하고 탄력적 toofailure입니다.

Azure 트래픽 관리자 응용 프로그램 끝점에서 트래픽의 toocontrol hello 배포를 사용합니다. 끝점은 Azure의 내부 또는 외부에서 호스팅되는 모든 인터넷 연결 서비스입니다.

Traffic Manager는 다음과 같은 두 가지 주요 이점을 제공합니다.

-   일부의 tooone에 따라 트래픽의 배포 [트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)합니다.

-   [끝점 상태 연속 모니터링](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) 및 끝점이 실패할 경우 자동 장애 조치(failover)

클라이언트가 tooconnect tooa 서비스 때 hello 서비스 tooan IP 주소의 DNS 이름을 hello를 먼저 해결 해야 합니다 것입니다. 클라이언트 hello toothat IP 주소 tooaccess hello 서비스를 연결합니다. 트래픽 관리자 사용 하 여 DNS toodirect 클라이언트 toospecific 서비스 hello 트래픽 라우팅 방법의 hello 규칙에 따라 끝점입니다. 클라이언트는 선택한 toohello 끝점을 직접 연결합니다. Traffic Manager는 프록시 또는 게이트웨이가 아닙니다. 트래픽 관리자는 클라이언트 hello와 hello 서비스 간에 전달 되는 hello 트래픽에 표시 되지 않습니다.

### <a name="azure-network-validation"></a>Azure 네트워크 유효성 검사

Azure 네트워크 유효성 검사는 구성 되 고 유효성 검사를 수행할 수 있습니다 하는 대로 Azure 네트워크 hello tooensure 작동 hello 서비스 및 기능 사용 가능한 toomonitor hello 네트워크를 사용 하 여 합니다. Azure 네트워크 감시자에 대 한 광범위 한 로깅 액세스할 수 있습니다 및 네트워크 성능 및 상태 insights toounderstand을 수행 하는 진단 기능입니다. 이러한 기능은 포털, Powershell, CLI, Rest API 및 SDK를 통해 액세스할 수 있습니다.

Azure Operational 보안 toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다. Azure Operational 보안 hello Microsoft SDL Security Development Lifecycle (), 보안 응답 센터 Microsoft hello 포함 하는 고유한 tooMicrosoft 있는 다양 한 기능을 통해 얻은 hello 정보를 통합 하는 프레임 워크에 만들어집니다. 프로그램 및 hello 사이버 보안 위협 상황의 심층 인식 합니다.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [ 분석](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure 리소스 관리자

#### <a name="azure-resource-manager"></a>Azure Resource Manager

hello 사람 및 Microsoft Azure 작동 하는 프로세스는 아마도 hello 플랫폼의 hello 가장 중요 한 보안 기능입니다. 이 섹션에서는 보안, 연속성 및 개인 정보 보호를 강화하고 유지하는 데 도움이 되는 Microsoft의 글로벌 데이터 센터 인프라의 기능에 대해 설명합니다.

일반적으로 많은 구성 요소가 – 미정 가상 컴퓨터, 저장소 계정 및 가상 네트워크 또는 웹 응용 프로그램, 데이터베이스, 데이터베이스 서버 및 공급 업체 서비스의 응용 프로그램에 대 한 hello 인프라 구성 됩니다. 이러한 구성 요소를 별도 엔터티로 표시하지 않으면, 대신 관련된 단일 엔터티의 상호 종속적으로 부분으로 표시됩니다. Toodeploy, 관리, 한 그룹으로 보고 모니터링 합니다. Azure 리소스 관리자 그룹으로 toowork 솔루션에 hello 리소스를 사용 합니다.

배포 지정, 업데이트 또는 단일, 통합 작업에서 솔루션에 대 한 모든 hello 리소스를 삭제 합니다. 배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다. 리소스 관리자는 감사 보안을 제공 하 고 리소스 배포 된 후 관리 기능 toohelp 태그를 지정 합니다.

**리소스 관리자를 사용 하 여 hello 이점**

리소스 관리자는 다음과 같은 여러 이점이 있습니다.

-   배포, 관리 하 고 이러한 리소스를 개별적으로 처리 하지 않고 그룹에서 솔루션에 대 한 모든 hello 리소스를 모니터링할 수 있습니다.

-   반복 해 서 hello 개발 수명 주기 전체에서 솔루션을 배포할 수 있으며 것을 확신할 리소스 일관 된 상태로 배포 됩니다.

-   스크립트가 아닌 선언적 템플릿을 통해 인프라를 관리할 수 있습니다.

-   Hello 올바른 순서로 배포 되므로 리소스 간의 종속성을 hello를 정의할 수 있습니다.

-   역할 기반 액세스 제어 (RBAC) hello 관리 플랫폼에 고유 하 게 통합 되어 있으므로 리소스 그룹에 대 한 액세스 제어 tooall 서비스를 적용할 수 있습니다.

-   태그를 적용할 수 tooresources toologically 구독에서 모든 hello 리소스를 구성 합니다.

-   태그를 공유하는 리소스 그룹에 대한 비용을 확인하여 조직의 청구를 명확히 할 수 있습니다.

> [!Note]
> 리소스 관리자는 새로운 방식으로 toodeploy 제공 하 고 솔루션을 관리 합니다. 사용 하는 경우 이전 버전의 배포 모델을 hello 및 toolearn hello 변경에 대 한 원하는, 참조 [이해 리소스 관리자 배포 및 클래식 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)합니다.

## <a name="azure-network-logging-and-monitoring"></a>Azure 네트워크 로깅 및 모니터링

Azure는 여러 도구 toomonitor, 방지, 검색 및 toonetwork 보안 이벤트에 응답 합니다. 이 영역의 hello 제공 하는 도구 가장 강력한 사용 가능한 tooyou 다음과 같습니다.

-   Network Watcher

-   네트워크 리소스 수준 모니터링

-   Log Analytics

### <a name="network-watcher"></a>Network Watcher

[네트워크 감시자](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -모니터링 시나리오 기반 네트워크 감시자의 hello 기능과 함께 제공 됩니다. 이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다. 수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.

네트워크 감시자는 현재 hello 기능 뒤에 있습니다.

#### <a name="topology"></a>토폴로지

[토폴로지](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview)는 가상 네트워크에서 네트워크 리소스의 그래프를 반환합니다. hello 그래프에는 hello 리소스 toorepresent hello 끝 tooend 네트워크 연결 사이의 hello를 상호 연결 합니다. Hello 포털 토폴로지 가상 네트워크 기준에 따라에 hello 리소스 개체를 반환합니다. hello 관계에서 hello 리소스 그룹은 표시 되지 않더라도 hello 네트워크 감시자 영역 외부의 hello 리소스 간의 선으로 표시 됩니다. hello hello 포털 뷰에서 반환 된 리소스가 그래프로 표현 하는 hello 네트워킹 구성의 하위 집합입니다. 사용할 수 있는 네트워킹 리소스의 toosee hello의 전체 목록, [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) 또는 [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest)합니다.

리소스가 반환 되 면 이러한 간의 hello 연결에서 두 개의 관계를 모델링 됩니다.

- **포함** - Virtual Network는 NIC를 포함하는 서브넷을 포함합니다.

- **연결됨** - NIC는 VM과 연결됩니다.

#### <a name="variable-packet-capture"></a>가변 패킷 캡처

네트워크 감시자 [변수 패킷 캡처](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) toocreate 패킷 캡처 세션 tootrack 트래픽 tooand 가상 컴퓨터를 수 있습니다. 패킷 캡처 프로비저닝하지 toodiagnose 네트워크 비정상 모두 사용 하면 proactivity 및 합니다. 통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.

패킷 캡처는 Network Watcher를 통해 원격으로 시작되는 가상 컴퓨터 확장입니다. 이 기능은 중요 한 시간을 절약할 hello 필요한 가상 컴퓨터에서 패킷 캡처를 수동으로 실행의 hello 부담을 줄일 수 있습니다. Hello 포털, PowerShell, CLI 또는 REST API를 통해 패킷 캡처를 트리거할 수 있습니다. 패킷 캡처를 트리거하는 방식에 대한 한 가지 예는 Virtual Machine 경고를 사용하는 것입니다.

#### <a name="ip-flow-verify"></a>IP 흐름 확인

[IP 흐름 확인](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) 패킷을 허용 또는 tooor 5-튜플 정보에 따라 가상 컴퓨터를 거부 하는 경우를 확인 합니다. 이 정보는 방향, 프로토콜, 로컬 IP, 원격 IP, 로컬 포트 및 원격 포트로 구성됩니다. Hello 패킷 보안 그룹에 의해 거부 되 면 hello 패킷을 거부 하는 hello 규칙의 hello 이름이 반환 됩니다. 모든 소스 또는 대상 IP를 선택한이 기능 하는 데 도움이에서 연결 문제 또는 toohello 신속 하 게 진단 하는 관리자가 인터넷에서 또는 toohello 온-프레미스 환경입니다.

IP 흐름 확인은 가상 컴퓨터의 네트워크 인터페이스를 대상으로 합니다. 트래픽 흐름에서 해당 네트워크 인터페이스 설정 tooor hello 구성에 따라 확인 됩니다. 이 기능은 네트워크 보안 그룹의 규칙은 가상 컴퓨터에서 수신 또는 송신 트래픽 tooor를 차단 하 고 하는 경우를 확인 하는 데 유용 합니다.

#### <a name="next-hop"></a>다음 홉

Hello 결정 [다음 홉](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) 패킷의 hello Azure 네트워크 패브릭 라우팅되는 사용자 정의 경로 잘못 구성 어떤 toodiagnose 있습니다를 사용 하도록 설정 합니다. 트래픽이 VM에서 NIC와 관련 된 hello 유효 경로에 따라 tooa 대상 전송 다음 홉에서 특정 가상 컴퓨터 및 NIC. hello 다음 홉 형식이 및 패킷의 IP 주소를 가져옵니다. 이렇게 하면 hello 패킷 되 toohello 방향이 지정 된 대상 또는 black 되 고 hello 트래픽 숨어 경우 toodetermine 있습니다.

또한 다음 홉 hello 다음 홉와 관련 된 hello 경로 테이블을 반환 합니다. 다음 홉을 hello 경로 사용자 정의 경로로 정의 된 경우 쿼리할 때 해당 경로 반환 됩니다. 그렇지 않은 경우 다음 홉은 "시스템 경로"를 반환합니다.

#### <a name="security-group-view"></a>보안 그룹 보기

VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다. 네트워크 보안 그룹은 서브넷 수준 또는 NIC 수준에서 연결됩니다. 서브넷 수준에서 연결 된, tooall hello VM 인스턴스 hello 서브넷에 적용 됩니다. 네트워크 [보안 그룹 보기](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) 모든 구성 hello Nsg와 hello 구성에 대 한 정보를 제공 하는 가상 컴퓨터에 대 한 서브넷과 NIC 수준에서 연결 된 규칙을 반환 합니다. 또한 hello 효과적인 보안 규칙은 VM에서 nic hello 각각에 대해 반환 됩니다. 네트워크 보안 그룹 보기를 사용하여 열린 포트와 같은 네트워크 취약점에 대해 VM을 평가할 수 있습니다. 네트워크 보안 그룹에 따라 예상 대로 작동 하는 경우에 확인할 수 있습니다는 [hello 간의 비교는 구성 하 고 효과적인 보안 규칙 hello](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell)합니다.

#### <a name="nsg-flow-logging"></a>NSG 흐름 로깅

 네트워크 보안 그룹에 대 한 흐름 로그를 사용 하면 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic 있습니다. hello 흐름은 5-튜플 정보 – 원본 IP, 대상 IP, 원본 포트, 대상 포트 및 프로토콜에 의해 정의 됩니다.

[네트워크 보안 그룹 흐름 로그](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Virtual Network 게이트웨이 및 연결 문제 해결

네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다. 이러한 기능 중 하나는 리소스 문제 해결입니다. [리소스 문제 해결](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)은 PowerShell, CLI 또는 REST API에서 호출될 수 있습니다. 호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.

이 섹션에서는 문제 해결 리소스에 대 한 현재 사용할 수 있는 hello 다른 관리 작업을 안내 합니다.

-   [Virtual Network 게이트웨이 문제 해결](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [연결 문제 해결](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>네트워크 구독 제한

[구독 제한 네트워크](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) hello 사용할 수 있는 리소스의 최대 수와 지역에서 구독에 hello 네트워크 리소스의 각 hello 사용량의 세부 정보를 제공 합니다.

#### <a name="configuring-diagnostics-log"></a>진단 로그 구성

Network Watcher는 [진단 로그](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) 보기를 제공합니다. 이 보기에는 진단 로깅을 지원하는 모든 네트워킹 리소스가 포함됩니다. 이 보기에서 네트워킹 리소스를 빠르고 편리하게 사용하거나 사용하지 않도록 설정할 수 있습니다.

### <a name="network-resource-level-monitoring"></a>네트워크 리소스 수준 모니터링

같은 기능 hello 리소스 수준 모니터링을 위해 사용할 수 있습니다.

#### <a name="audit-log"></a>감사 로그

네트워크의 hello 구성의 일부분으로 수행 되는 작업 기록 됩니다. 이러한 감사 로그는 필수적인 tooestablish 다양 한 규정을 준수 합니다. 이러한 로그는 hello Azure 포털에서에서 볼 수 있습니다 또는 Power BI와 같은 Microsoft 도구 또는 타사 도구를 사용 하 여 검색 합니다. 감사 로그는 hello 포털, PowerShell, CLI 및 Rest API를 통해 사용할 수 있습니다.

> [!Note]
> 감사 로그에 대한 자세한 내용은 ["Resource Manager로 작업 감사"](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit)를 참조하세요.
감사 로그는 모든 네트워크 리소스에서 수행된 작업에 사용할 수 있습니다.


#### <a name="metrics"></a>메트릭

메트릭은 일정 기간 동안 수집된 성능 측정 및 카운터입니다. 메트릭은 현재 Application Gateway에서 사용할 수 있습니다. 메트릭은은 tootrigger 사용 되는 경고 임계값에 기반을 수 있습니다. 기본적으로 azure 응용 프로그램 게이트웨이 응용 프로그램은 백 엔드 풀의 모든 리소스의 hello 상태를 모니터링 하 고 자동으로 hello 풀에서 비정상으로 간주 하는 모든 리소스를 제거 합니다. 응용 프로그램 게이트웨이 toomonitor hello 비정상 인스턴스를 계속 하 고 해당 추가 사용 가능 하 게 하 고 응답 toohealth 프로브 toohello 정상 백 엔드 풀을 백업 합니다. 응용 프로그램 게이트웨이 백 엔드 HTTP 설정 hello에에서 정의 된 동일한 포트 hello로 hello 상태 프로브를 보냅니다. 이 구성을 통해 해당 hello 프로브 hello 동일한 포트 고객 tooconnect toohello 백 엔드 사용 될 수 있는지 테스트 하는 것입니다.

> [!Note]
> 참조 [응용 프로그램 게이트웨이 진단](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview 어떻게 메트릭을 사용 하는 toocreate 경고 수입니다.

#### <a name="diagnostic-logs"></a>진단 로그

정기적이 고 비 정기적인 이벤트는 네트워크 리소스에 의해 생성 및 tooan 이벤트 허브 또는 로그 분석을 전송 하는 저장소 계정에 기록 됩니다. 이러한 로그는 리소스의 hello 상태에 대 한 정보를 제공합니다. Power BI 및 Log Analytics와 같은 도구에서 볼 수 있습니다. tooview 진단 로그를 방문 하는 방법을 toolearn [로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)합니다.

진단 로그는 [부하 분산 장치](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), 경로 및 [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)에서 사용할 수 있습니다.

Network Watcher는 진단 로그 보기를 제공합니다. 이 보기에는 진단 로깅을 지원하는 모든 네트워킹 리소스가 포함됩니다. 이 보기에서 네트워킹 리소스를 빠르고 편리하게 사용하거나 사용하지 않도록 설정할 수 있습니다.

### <a name="log-analytics"></a>Log Analytics

[로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) 에서 서비스가 [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 프로그램 클라우드 및 온-프레미스 환경 toomaintain의 가용성과 성능을 모니터링 하는 합니다. 여러 소스에서 리소스를 클라우드 및 온-프레미스 환경에서와 다른 모니터링 도구 tooprovide 분석에 의해 생성 된 데이터를 수집 합니다.

로그 분석은 hello 다음 실제 네트워크 모니터링을 위해 솔루션을 제공 합니다.

-   NPM(네트워크 성능 모니터)

-   Azure Application Gateway 분석

-   Azure 네트워크 보안 그룹 분석

#### <a name="network-performance-monitor-npm"></a>NPM(네트워크 성능 모니터)
hello [네트워크 성능 모니터](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) 관리 솔루션은 네트워크 hello 상태, 가용성 및 네트워크 연결 가능성을 모니터링 하는 솔루션을 모니터링 합니다.

간의 toomonitor 사용 되는 연결입니다.

-   공용 클라우드 및 온-프레미스

-   데이터 센터와 사용자 위치(지점)

-   다중 계층 응용 프로그램의 다양한 계층을 호스팅하는 서브넷


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Log Analytics의 Azure Application Gateway 분석

응용 프로그램 게이트웨이 로그 다음 hello 지원 됩니다.

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

응용 프로그램 게이트웨이 hello 다음 메트릭을 지원 됩니다.

-   5분 처리량

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Log Analytics의 Azure 네트워크 보안 그룹 분석

hello 다음 로그는 지원에 대 한 [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** 어떤 NSG에 대 한 규칙은 적용 된 tooVMs 및 MAC 주소에 따라 인스턴스 역할 항목을 포함 합니다. 이러한 규칙에 대 한 hello 상태 60 초 마다 수집 됩니다.

- **NetworkSecurityGroupRuleCounter:** Contains 항목 각 NSG 횟수에 대 한 규칙을 적용 된 toodeny 되었거나 트래픽을 허용 합니다.

## <a name="next-steps"></a>다음 단계
다음과 같은 심층적인 일부 보안 항목을 참조하여 보안에 대한 자세한 내용을 확인할 수 있습니다.

-   [NSG(네트워크 보안 그룹)에 대한 Log Analytics](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [해당 드라이브 hello 클라우드 중단 혁신 사항과 네트워킹](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [네트워킹 전역 클라우드 Microsoft hello를 구동 하는 스위치가 소프트웨어 SONiC: hello](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Microsoft에서 빠르고 신뢰할 수 있는 글로벌 네트워크를 구축하는 방법](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [네트워크 혁신 조명](https://azure.microsoft.com/blog/lighting-up-network-innovation/)

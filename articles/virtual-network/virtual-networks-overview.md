---
title: "가상 네트워크 aaaAzure | Microsoft Docs"
description: "Azure Virtual Network 개념 및 기능에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Azure Virtual Network

안녕 toosecurely 하면 가상 네트워크 (Vnet)를 사용 하 여 다른 Azure 리소스 tooeach를 연결 하는 Azure 가상 네트워크 서비스 수 있습니다. VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet의 hello Azure 클라우드 전용 tooyour 구독 논리적 격리입니다. 또한 Vnet tooyour 온-프레미스 네트워크를 연결할 수 있습니다. 다음 그림 hello hello Azure 가상 네트워크 서비스의 hello 기능 중 일부를 보여 줍니다.

![네트워크 다이어그램](./media/virtual-networks-overview/virtual-network-overview.png)

Azure 가상 네트워크 기능을 수행 하는 hello에 대 한 자세한 toolearn hello 기능을 클릭 합니다.
- **[격리:](#isolation)** VNet은 서로 격리되어 있습니다. 사용 하 여 hello 개발, 테스트 및 프로덕션에 대 한 별도 Vnet에 만들 수 같은 CIDR 주소 블록입니다. 반대로, 여러 CIDR 주소 블록을 사용하는 VNet을 만들어 네트워크를 서로 연결할 수도 있습니다. VNet은 여러 서브넷으로 분할할 수 있습니다. 클라우드 서비스 역할 인스턴스 tooa VNet 연결 및 azure Vm에 대 한 내부 이름 확인을 제공 합니다. 필요에 따라 VNet toouse Azure 내부 이름 확인을 사용 하는 대신 고유한 DNS 서버를 구성할 수 있습니다.
- **[인터넷 연결:](#internet)**  연결 된 VNet tooa 있어야 하는 모든 Azure 가상 컴퓨터 (VM) 및 클라우드 서비스 역할 인스턴스 기본적으로 toohello 인터넷에 액세스 합니다. 필요에 따라 toospecific 리소스에 인바운드 액세스를 설정할 수도 있습니다.
- **[Azure 리소스 연결:](#within-vnet)**  클라우드 서비스 및 Vm와 같은 Azure 리소스에 연결 된 toohello 수 동일한 VNet입니다. hello 리소스 다른 tooeach 연결할 수 있는 개인 IP를 사용 하 여 주소, 서브넷이 서로 다른 경우에 합니다. Azure 없습니다 tooconfigure 하 고 경로 관리 하므로 기본 서브넷, Vnet 및 온-프레미스 네트워크 간의 라우팅을 제공 합니다.
- **[VNet 연결:](#connect-vnets)**  Vnet에는 다른 연결 된 tooeach 수 있으며, tooany VNet toocommunicate 다른 VNet에 리소스와 연결 된 리소스를 사용 하도록 설정 합니다.
- **[온-프레미스 연결:](#connect-on-premises)**  Vnet hello 인터넷을 통해 네트워크와 Azure 간의 개인 네트워크 연결을 통해 또는 사이트 간 VPN 연결을 통해 네트워크에 연결 된 tooon 온-프레미스 네트워크를 수 있습니다.
- **[트래픽 필터링:](#filtering)** VM 및 Cloud Services 역할 인스턴스 네트워크 트래픽을 원본 IP 주소 및 포트, 대상 IP 주소 및 포트, 그리고 프로토콜별로 인바운드 및 아웃바운드에 따라 필터링할 수 있습니다.
- **[라우팅:](#routing)** 필요에 따라 자체 경로를 구성하거나 네트워크 게이트웨이 통한 BGP 경로의 사용으로 Azure의 기본 라우팅을 재정의할 수 있습니다.

## <a name = "isolation"></a>네트워크 격리 및 분할

각 Azure [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 및 Azure [지역](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region) 내에서 여러 VNet을 구현할 수 있습니다. 각 VNet은 다른 VNet에서 격리됩니다. 각 VNet에 대해 다음을 수행할 수 있습니다.
- 공용 및 사설(RFC 1918) 주소를 사용하여 사용자 지정 사설 IP 주소 공간을 지정합니다. Azure는 리소스 연결된 toohello VNet 개인 IP 주소를 할당 하는 hello 주소 공간에서 할당 합니다.
- Hello VNet 주소 공간 tooeach 서브넷의 일부를 할당 하 고 hello VNet 하나 이상의 서브넷으로 분할 합니다.
- Azure 제공 이름 확인을 사용 하거나 tooa VNet를 연결 하는 리소스에서 사용 하기 위해 자체 DNS 서버 지정 합니다. hello 읽을 Vnet에서 이름 확인에 대 한 자세한 toolearn [Vm 및 클라우드 서비스에 대 한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서.

## <a name = "internet"></a>Toohello 인터넷 연결
모든 리소스 연결된 tooa VNet 기본적으로 인터넷 아웃 바운드 연결 toohello가 있어야 합니다. hello hello 리소스의 개인 IP 주소는 원본 네트워크 주소 hello Azure 인프라에 의해 (SNAT) tooa 공용 IP 주소를 변환 합니다. hello 읽을 아웃 바운드 인터넷 연결에 대 한 자세한 toolearn [Azure의 아웃 바운드 연결 이해](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) 문서. 사용자 지정 라우팅 및 트래픽 필터링을 구현 하 여 hello 기본 연결을 변경할 수 있습니다.

toocommunicate 인바운드 tooAzure 리소스에서 인터넷을 hello 또는 toocommunicate 아웃 바운드 toohello SNAT, 리소스 없이 인터넷에 공용 IP 주소를 할당 해야 합니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [공용 IP 주소](virtual-network-public-ip-address.md) 문서.

## <a name="within-vnet"></a>Azure 리소스 연결
여러 Azure 리소스 tooa 가상 컴퓨터 (VM), 클라우드 서비스, 앱 서비스 환경 및 가상 컴퓨터 크기 집합 같이 VNet을 연결할 수 있습니다. Vm은 네트워크 인터페이스 (NIC)를 통해 VNet 내의 서브넷 tooa를 연결합니다. hello 읽을 Nic에 대 한 자세한 toolearn [네트워크 인터페이스](virtual-network-network-interface.md) 문서.

## <a name="connect-vnets"></a>가상 네트워크 연결

다른 Vnet tooeach 연결할 수 있습니다, Vnet에 걸쳐 서로 tooeither VNet toocommunicate 연결 리소스를 사용 하도록 설정 합니다. Hello 옵션 tooconnect Vnet tooeach 다른 다음 중 하나 또는 모두를 사용할 수 있습니다.
- **피어 링:** 사용 리소스 연결 hello 내에서 Azure Vnet toodifferent 서로 동일한 Azure 위치 toocommunicate 합니다. hello 대역폭 및 대기 시간 Vnet은 hello 간에 hello 동일 하면 hello 리소스에 연결 된 toohello 것 처럼 동일한 VNet입니다. 피어 링을 대 한 자세한 toolearn 읽을 hello [가상 네트워크 피어 링](virtual-network-peering-overview.md) 문서.
- **VNet 대 VNet 연결:** 사용 리소스 연결 hello 내에서 Azure VNet toodifferent 같거나 다른 Azure 위치입니다. 피어링과 달리, 트래픽이 Azure VPN Gateway를 통과해야 하기 때문에 VNet 간에 대역폭이 제한됩니다. Vnet hello 읽을 VNet 대 VNet 연결을 통해 연결 하는 방법에 대 한 자세한 toolearn [VNet 대 VNet 연결 구성](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.

## <a name="connect-on-premises"></a>Tooan 온-프레미스 네트워크에 연결

온-프레미스 네트워크 tooa hello 다음 옵션을 조합 하 여 VNet을 연결할 수 있습니다.
- **지점 및 사이트 간 가상 사설망 (VPN):** 간에 단일 PC tooyour 연결 된 네트워크 및 VNet hello를 설정 합니다. 이 연결 유형에 거의 또는 전혀 변경 tooyour 기존 네트워크 필요 하기 때문에 수행 하는 개발자를 위한 또는 azure를 하는 경우 유용 합니다. hello 연결 hello PC와 hello VNet 간의 인터넷 hello 통한 hello SSTP 프로토콜 암호화 tooprovide 통신을 사용합니다. hello 트래픽이 hello 인터넷에서 이동 하는 지점-사이트 VPN에 대 한 hello 대기 시간은 예측 가능 하지 않습니다.
- **사이트 간 VPN:** VPN 장치와 Azure VPN Gateway 간에 설정됩니다. 이 연결 유형에 모든 온-프레미스 리소스를 tooaccess VNet 권한을 부여할 수 있습니다. hello 연결은 온-프레미스 장치와 hello Azure VPN 게이트웨이 hello 인터넷을 통해 암호화 된 통신을 제공 하는 IPSec/IKE VPN입니다. 사이트 간 연결에 대 한 대기 시간 hello은 hello 트래픽이 트래버스하 hello 인터넷 예측 가능 하지 않습니다.
- **Azure ExpressRoute:** ExpressRoute 파트너를 통해 네트워크와 Azure 간에 설정됩니다. 이 연결은 사설 전용입니다. 트래픽 hello 인터넷을 통과 하지 않는 합니다. ExpressRoute 연결에 대 한 hello 대기 시간, 예측 가능한 없으므로 트래픽 hello 인터넷을 트래버스 하지 않습니다.

모든 hello 이전 연결 옵션을 hello 읽기에 대 한 자세한 toolearn [연결 토폴로지 다이어그램](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) 문서.

## <a name="filtering"></a>네트워크 트래픽 필터링
Hello 다음 옵션 중 하나 또는 모두를 사용 하 여 서브넷 간의 네트워크 트래픽을 필터링 할 수 있습니다.
- **네트워크 보안 그룹 (NSG):** 각 NSG에는 원본 및 대상 IP 주소, 포트 및 프로토콜 toofilter 트래픽 수 있도록 하는 여러 개의 인바운드 및 아웃 바운드 보안 규칙 포함 될 수 있습니다. NSG tooeach VM에서 NIC에 적용할 수 있습니다. 다른 Azure 리소스에 연결 되어 또는 NIC에 NSG toohello 서브넷도 적용할 수 있습니다. hello 읽을 Nsg에 대 한 자세한 toolearn [네트워크 보안 그룹](virtual-networks-nsg.md) 문서.
- **NVA(네트워크 가상 어플라이언스):** NVA는 방화벽과 같은 네트워크 기능을 수행하는 소프트웨어를 실행하는 VM입니다. Hello에서 사용할 수 있는 NVAs의 목록을 볼 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)합니다. WAN 최적화 및 기타 네트워크 트래픽 기능을 제공하는 NVA도 사용할 수 있습니다. NVA는 일반적으로 사용자 정의 경로 또는 BGP 경로와 함께 사용됩니다. 또한 Vnet 간의 NVA toofilter 트래픽을 사용할 수 있습니다.

## <a name="routing"></a>네트워크 트래픽 라우팅

Azure에서는 기본적으로, 모든 VNet toocommunicate에서 리소스 연결 된 tooany 서브넷을 사용할 수 있는 경로 테이블을 만듭니다. 구현할 수 있습니다 또는 둘 다의 hello 옵션 toooverride 다음 hello Azure 만듭니다 기본 경로:
- **사용자 정의 경로:** 각 서브넷 트래픽이 라우팅된 toofor가 제어 하는 경로 가진 사용자 지정 경로 테이블을 만들 수 있습니다. hello 읽기 사용자 정의 경로 대 한 자세한 toolearn [사용자 정의 경로](virtual-networks-udr-overview.md) 문서.
- **BGP 경로:** Azure VPN 게이트웨이 또는 express 경로 연결을 사용 하 여 VNet tooyour 온-프레미스 네트워크를 연결 하는 경우 BGP 경로 tooyour Vnet에 전파할 수 있습니다.

## <a name="pricing"></a>가격

가상 네트워크, 서브넷, 경로 테이블 또는 네트워크 보안 그룹은 무료입니다. 아웃바운드 인터넷 대역폭 사용량, 공용 IP 주소, 가상 네트워크의 피어링, VPN Gateway 및 ExpressRoute 각각에는 자체적인 가격 책정 체계가 설정되어 있습니다. 보기 hello [가상 네트워크](https://azure.microsoft.com/pricing/details/virtual-network), [VPN 게이트웨이](https://azure.microsoft.com/pricing/details/vpn-gateway), 및 [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) 가격에 대 한 자세한 내용은 페이지입니다.

## <a name="faq"></a>FAQ

가상 네트워크에 대 한 질문과 대답 tooreview 참조 hello [가상 네트워크 FAQ](virtual-networks-faq.md) 문서.


## <a name="next-steps"></a>다음 단계

- 첫 번째 VNet을 만들고 몇 가지 Vm tooit hello의 hello 단계를 완료 하 여 연결 [첫 번째 가상 네트워크를 만든](virtual-network-get-started-vnet-subnet.md) 문서.
- Hello의 hello 단계를 완료 하 여 지점 및 사이트 연결 tooa VNet을 만들 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.
- 일부 hello에 대 한 자세한 내용은 다른 키 [네트워크 기능](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure의 합니다.

---
title: "VPN 게이트웨이 개요: tooAzure 가상 네트워크 크로스-프레미스 VPN 연결 만들기 | Microsoft Docs"
description: "이 VPN 게이트웨이 개요 hello 방법으로 tooconnect tooAzure 가상 네트워크 VPN 연결을 사용 하 여 hello 인터넷을 통해 설명 합니다. 기본 연결 구성의 다이어그램이 포함됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>VPN Gateway 정보

VPN 게이트웨이 가상 네트워크 게이트웨이 공용 연결 tooan 간에 암호화 된 트래픽을 온-프레미스 위치 보내는 유형입니다. 또한 hello Microsoft 네트워크를 통해 Azure 가상 네트워크 간의 VPN 게이트웨이 toosend 암호화 된 트래픽을 사용할 수 있습니다. Azure 가상 네트워크와 온-프레미스 사이트 간의 네트워크 트래픽을 암호화 toosend 만들어야 VPN 게이트웨이 가상 네트워크에 대 한 합니다.

하지만 각 가상 네트워크 VPN 게이트웨이 하나만 가질 수 있습니다, 여러 연결 toohello를 만들 수 있습니다 VPN 게이트웨이 동일한 합니다. 한 가지 예로 다중 사이트 연결 구성이 있습니다. 여러 연결 toohello를 만들 때 동일한 VPN 게이트웨이에 지점-사이트 Vpn, hello 게이트웨이에 사용할 수 있는 공유 hello 대역폭을 비롯 한 모든 VPN 터널 합니다.

### <a name="whatis"></a>가상 네트워크 게이트웨이란?

가상 네트워크 게이트웨이 두 이루어져 또는 더 많은 가상 컴퓨터 배포 hello GatewaySubnet 이라는 tooa 특정 서브넷. GatewaySubnet hello 가상 네트워크 게이트웨이 만들 때 함께 생성 되는 hello에 있는 Vm 번호입니다. 가상 네트워크 게이트웨이 Vm은 구성 된 toocontain 라우팅 테이블 및 특정 toohello 게이트웨이 서비스입니다. Hello hello 가상 네트워크 게이트웨이의 일부인 가상 컴퓨터를 직접 구성할 수 없습니다 및 추가 리소스 toohello GatewaySubnet 배포 하지 않아야 합니다.

특정 유형의 트래픽을 암호화 하는 가상 네트워크 게이트웨이 만듭니다 hello 게이트웨이 유형 'Vpn'를 사용 하 여 가상 네트워크 게이트웨이 만들 때 VPN 게이트웨이 합니다. VPN 게이트웨이 too45 분 toocreate 차지할 수 있습니다. Hello VPN 게이트웨이에 대 한 hello Vm 배포 toohello GatewaySubnet 되는 중 이므로 이며 지정한 hello 설정으로 구성 하십시오. 선택한 게이트웨이 SKU hello Vm은 얼마나 강력한 hello를 결정 합니다.

## <a name="gwsku"></a>게이트웨이 SKU

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>VPN Gateway 구성

VPN Gateway 연결은 특정 설정으로 구성된 여러 리소스에 따라 다릅니다. 일부 경우에는 특정 순서로 구성 해야 하지만 대부분의 hello 리소스 별도로 구성할 수 있습니다.

### <a name="settings"></a>설정

hello 각 리소스에 대해 선택한 설정이 중요 한 toocreating 성공적으로 연결 되었습니다. VPN Gateway의 개별 리소스 및 설정에 대한 정보는 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요. hello 문서 정보 toohelp을 게이트웨이 유형, VPN 유형, 연결 유형, 게이트웨이 서브넷, 로컬 네트워크 게이트웨이 및 기타 다양 한 리소스 설정을 tooconsider를 취소할 수 있음을 이해 하 나와 있습니다.

### <a name="tools"></a>배포 도구

만들고 Azure 포털 hello 등과 같은 하나의 구성 도구를 사용 하 여 리소스를 구성 하는 아웃 시작할 수 있습니다. 나중에 PowerShell, tooconfigure 추가 리소스 등 tooswitch tooanother 도구를 결정 하거나 해당 하는 경우 기존 리소스를 수정할 수 있습니다. 현재 hello Azure 포털에서에서 모든 리소스 및 리소스 설정을 구성할 수 없습니다. 각 연결 토폴로지에 대 한 hello 아티클의 hello 지침에는 특정 구성 도구가 필요한 경우를 지정 합니다. 

### <a name="models"></a>배포 모델

VPN 게이트웨이 구성할 때 수행 하는 hello 단계에 따라 다릅니다 hello 배포 모델을 사용 하 여 toocreate 가상 네트워크. 예를 들어 VNet을 만들 경우 hello 클래식 배포 모델을 사용 하 여 hello 지침을 사용 하 고 hello 클래식 배포에 대 한 지침 toocreate 모델 VPN 게이트웨이 설정을 구성 합니다. 배포 모델에 대한 자세한 내용은 [Resource Manager 배포 및 클래식 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.

## <a name="diagrams"></a>연결 토폴로지 다이어그램

것이 중요 한 tooknow VPN 게이트웨이 연결에 사용할 수 있는 다른 여러 구성을 지 합니다. 필요에 맞는 최적의 구성을 toodetermine가 필요 합니다. Hello 섹션 아래에서 VPN 게이트웨이 연결을 수행 하는 hello에 대 한 정보 및 토폴로지 다이어그램을 볼 수 있습니다: 다음 섹션 hello 나열 하는 테이블을 포함 합니다.

* 사용 가능한 배포 모델
* 사용 가능한 구성 도구
* 연결 된 링크를 직접 tooan 문서, 사용 가능한 경우

사용 하 여 hello 다이어그램 및 설명이 toohelp 요구 사항 hello 연결 토폴로지 toomatch를 선택 합니다. hello 다이어그램에 표시 hello 주 초기 토폴로지 이지만 가능한 toobuild 지침으로 hello 다이어그램을 사용 하 여 보다 복잡 한 구성 합니다.

## <a name="s2smulti"></a>사이트 간 및 다중 사이트(IPsec/IKE VPN 터널)

### <a name="S2S"></a>사이트 간

S2S(사이트 간) VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통한 연결입니다. S2S 연결에는 VPN 장치에 있는 온-프레미스 NAT 내부의 및 공용 IP 주소 할당 tooit 필요 S2S 연결은 프레미스 간 및 하이브리드 구성에 사용될 수 있습니다.   

![Azure VPN Gateway 사이트 간 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>다중 사이트

이러한 종류의 연결에는 hello 사이트 간 연결의 변형입니다. 가상 네트워크 게이트웨이에서 둘 이상의 VPN 연결을 만드는, toomultiple를 연결 하는 일반적으로 온-프레미스 사이트입니다. 여러 연결을 사용하는 경우 경로 기반 VPN 유형(클래식 VNet을 사용하는 경우 동적 게이트웨이)을 사용해야 합니다. 각 가상 네트워크에서 하나의 VPN 게이트웨이 하나만 사용할 수 있습니다, 때문에 hello 게이트웨이 통해 모든 연결 hello 사용 가능한 대역폭을 공유 합니다. 이는 "다중 사이트" 연결이라고 합니다.

![Azure VPN Gateway 다중 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>사이트 간 및 다중 사이트의 배포 모델 및 메서드

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>지점 및 사이트 간(SSTP를 통한 VPN)

지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다. 지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다. P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다. 

S2S 연결과 달리 P2S 연결은 온-프레미스 공용 IP 주소 또는 VPN 장치가 필요하지 않습니다. P2S 연결을 통해 S2S 연결 사용 하 여 호환 되는 두 연결에 대 한 구성 요구 사항 hello 모든으로 동일한 VPN 게이트웨이에 hello 합니다.

P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다. Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.

![Azure VPN Gateway 지점 및 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>지점 및 사이트에 대한 배포 모델 및 메서드

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>VNet 간 연결(IPsec/IKE VPN 터널)

가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. VNet 간 통신을 다중 사이트 연결 구성과 통합할 수도 있습니다. 이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.

hello Vnet에 연결할 수 있습니다.

* hello에 같거나 다른 지역
* hello에 같거나 다른 데이터 집합 구독 
* hello에 같거나 다른 배포 모델

![Azure VPN 게이트웨이 VNet tooVNet 연결 예](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>배포 모델 간의 연결

Azure에는 현재 클래식 및 Resource Manager 등 두 개의 배포 모델이 있습니다. 일정 기간 동안 Azure를 사용한 경우 Azure VM 및 인스턴스 역할이 클래식 VNet에서 실행되고 있을 것입니다. 이후의 VM 및 역할 인스턴스는 Resource Manager에서 만들 VNet에서 실행되고 있을 것입니다. 다른 리소스와 직접 하나의 VNet toocommunicate에 hello Vnet tooallow 사이의 연결 hello 리소스를 만들 수 있습니다.

### <a name="vnet-peering"></a>VNet 피어링

가상 네트워크는 특정 요구 사항을 충족으로 수 toouse VNet toocreate 해당 연결을 피어 링을 수 있습니다. VNet 피어링은 가상 네트워크 게이트웨이를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>VNet 간 배포 모델 및 메서드

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute(전용 개인 연결)

Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 통해 지원 되는 전용된 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있습니다. ExpressRoute를 사용 Microsoft Azure, Office 365, CRM Online과 같은 연결 tooMicrosoft 클라우드 서비스를 설정할 수 있습니다. 공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다.

ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해.

ExpressRoute 연결은 필수 구성의 일부분으로 가상 네트워크 게이트웨이를 사용하지만 VPN Gateway는 사용하지 않습니다. ExpressRoute 연결에서 hello 가상 네트워크 게이트웨이 'Vpn' 대신 'ExpressRoute' hello 게이트웨이 유형으로 구성 됩니다. ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 기술 개요](../expressroute/expressroute-introduction.md)합니다.

## <a name="coexisting"></a>사이트 간 및 ExpressRoute 공존 연결

ExpressRoute는 WAN에서 직접는 전용된 연결 (하지 않고 공용 인터넷 hello) tooMicrosoft Azure를 포함 한 서비스를 합니다. 사이트-사이트 VPN 트래픽의 hello를 통해 암호화 여행 공용 인터넷 합니다. 되 고 수 tooconfigure 사이트 간 VPN 및 express 경로 연결 hello 동일한 가상 네트워크에 대해 여러 가지 이점이 있습니다.

ExpressRoute를에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성 하거나 네트워크의 일부가 아닌 하지만 ExpressRoute를 통해 연결 된 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다. 확인에 대 한 두 가상 네트워크 게이트웨이 hello 동일한 가상 네트워크, hello 게이트웨이 유형 'Vpn' 및 'ExpressRoute' hello 게이트웨이 유형을 사용 하 여 hello를 사용 하 여이 구성에 필요 합니다.

![ExpressRoute 및 VPN Gateway 공존 연결 예제](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>S2S 및 ExpressRoute에 대한 배포 모델 및 메서드

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>가격

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

VPN Gateway용 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.

## <a name="faq"></a>FAQ

VPN 게이트웨이에 대 한 자주 묻는 질문에 대 한 참조 hello [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md)합니다.

## <a name="next-steps"></a>다음 단계

- VPN Gateway 구성을 계획합니다. [VPN Gateway 계획 및 설계](vpn-gateway-plan-design.md)를 참조하세요.
- 보기 hello [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md) 추가 정보에 대 한 합니다.
- 보기 hello [구독 및 서비스 제한](../azure-subscription-service-limits.md#networking-limits)합니다.
- 일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.

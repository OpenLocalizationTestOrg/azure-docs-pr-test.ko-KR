---
title: "Azure VPN 게이트웨이 사용 하는 항상 사용 가능한 구성 aaaOverview | Microsoft Docs"
description: "이 문서에서는 Azure VPN Gateway를 사용하여 항상 사용 가능한 구성 옵션의 개요를 제공합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>항상 사용 가능한 크로스-프레미스 및 VNet 간 연결
이 문서에서는 Azure VPN Gateway를 사용하여 크로스-프레미스 및 VNet 간 연결에 대해 항상 사용 가능한 구성 옵션의 개요를 제공합니다.

## <a name = "activestandby"></a>Azure VPN Gateway 중복 정보
모든 Azure VPN Gateway는 활성-대기 구성 상태에 있는 두 인스턴스로 구성됩니다. 모든 계획 된 유지 관리 또는 toohello 활성 인스턴스에서 발생 하는 계획 되지 않은 중단에 대 한 hello 대기 인스턴스 (장애 조치)를 통해 자동으로 수행 하 고 hello S2S VPN 또는 VNet 대 VNet 연결을 다시 시작 게 됩니다. hello 전환은 중단을 발생 합니다. 계획 된 유지 관리에 대 한 10 too15 초 이내 hello 연결을 복원 해야 합니다. 계획 되지 않은 문제에 대 한 hello 연결 복구를 1 분 too1에 대 한 긴 수 및 hello 최악의 경우에서 30 분 시간 (분)입니다. P2S VPN 클라이언트 연결 toohello 게이트웨이에 대 한 hello P2S 연결이 끊어지고 hello 사용자가 tooreconnect hello 클라이언트 컴퓨터에서 필요 합니다.

![활성-대기](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>항상 사용 가능한 크로스-프레미스 연결
tooprovide 더 나은 가용성에 대 한 사용자 크로스 프레미스 연결, 사용 가능한 두 가지 옵션이 있습니다.

* 다중 온-프레미스 VPN 장치
* 활성-활성 Azure VPN Gateway
* 둘의 조합

### <a name = "activeactiveonprem"></a>다중 온-프레미스 VPN 장치
Hello 다음 다이어그램에에서 나와 있는 것 처럼 온-프레미스 네트워크 tooconnect tooyour Azure VPN 게이트웨이에서 여러 VPN 장치를 사용할 수 있습니다.

![다중 온-프레미스 VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

이 구성은 제공 hello에서 여러 활성 터널 hello에 동일한 Azure VPN 게이트웨이 tooyour 온-프레미스 장치 동일한 위치입니다. 요구 사항 및 제약 조건은 다음과 같습니다.

1. Toocreate 여러 S2S VPN 연결에서에서 필요한 VPN 장치 tooAzure 합니다. Hello에서 여러 VPN 장치를 연결할 때 동일한 온-프레미스 네트워크 tooAzure, Azure VPN 게이트웨이 toohello 로컬 네트워크 게이트웨이에서 toocreate 각 VPN 장치에 대 한 로컬 네트워크 게이트웨이 및 하나의 연결이 필요 합니다.
2. tooyour VPN 장치에 해당 하는 hello 로컬 네트워크 게이트웨이 hello "GatewayIpAddress" 속성에에서 고유한 공용 IP 주소를 있어야 합니다.
3. BGP가 이 구성에 필요합니다. VPN 장치를 나타내는 각 로컬 네트워크 게이트웨이 hello "BgpPeerIpAddress" 속성에 지정 하는 고유한 BGP 피어 IP 주소가 있어야 합니다.
4. 각 로컬 네트워크 게이트웨이 hello AddressPrefix 속성 필드를 겹치지 않아야 합니다. "BgpPeerIpAddress" hello/32에서 지정 해야 hello AddressPrefix 필드에서 예를 들어 10.200.200.254/32 CIDR 형식입니다.
5. BGP를 사용 해야 tooadvertise hello 동일한 접두사가 동일한 온-프레미스 네트워크 접두사 tooyour Azure VPN 게이트웨이 hello의 및 동시에 hello 트래픽 이러한 터널을 통해 전달 됩니다.
6. Hello Azure VPN 게이트웨이, Basic 및 Standard Sku에 대 한 10에 대 한 터널의 최대 수와 각 연결을 계산 및 HighPerformance SKU에 대 한 30입니다. 

이 구성에서는 hello Azure VPN 게이트웨이 아직 활성-대기 모드에에서는, 동일한 장애 조치 동작 하므로 hello 및 잠깐 중단 된 여전히 발생 하는 설명 된 대로 [위에](#activestandby)합니다. 하지만 이 설정을 통해 온-프레미스 네트워크 및 VPN 장치에서 실패 또는 중단되지 않도록 보호합니다.

### <a name="active-active-azure-vpn-gateway"></a>활성-활성 Azure VPN Gateway
이제 Vm에서는 S2S VPN 다음 표시 된 hello로 tooyour 온-프레미스 VPN 장치 터널을 설정 하는 hello 게이트웨이의 두 인스턴스가 다이어그램에 활성-활성 구성에 있는 Azure VPN 게이트웨이 만들 수 있습니다.

![활성-활성](./media/vpn-gateway-highlyavailable/active-active.png)

이 구성에서는 각 Azure 게이트웨이 인스턴스 문자열 고유한 공용 IP 주소를가지고 있으며는 IPsec/IKE S2S VPN 터널 tooyour 온-프레미스 VPN 장치 로컬 네트워크 게이트웨이 및 연결에 지정 된을 설정할 각각. 두 VPN 터널 hello에 실제로 포함 하는 동일한 연결 합니다. 계속 하면 온-프레미스 VPN 장치 tooaccept tooconfigure 필요 되거나 두 S2S VPN 터널 toothose 두 Azure VPN 게이트웨이 공용 IP 주소를 설정 됩니다.

Hello Azure 게이트웨이 인스턴스가 활성-활성 구성에 있으므로 Azure 가상 네트워크 tooyour hello 트래픽 온-프레미스 네트워크 라우팅될 두 터널을 통해 동시에 온-프레미스 VPN 장치 수 하나의 터널을 우선적 하는 경우에 hello 다른 합니다. 참고는 hello 동일한 TCP 또는 UDP 흐름을 트래버스할 항상 있지만 hello 동일한 터널 또는 경로 유지 관리 이벤트 hello 인스턴스 중 하나에서 발생 하지 않는 한 합니다.

계획 된 유지 관리 또는 계획 되지 않은 이벤트 tooone 게이트웨이 인스턴스 경우 해당 인스턴스 tooyour에서 hello IPsec 터널 온-프레미스 VPN 장치를 분리 됩니다. hello VPN 장치에서 해당 경로 제거 되거나 되어서는 hello 트래픽을 통해 toohello 전환 됩니다 되도록 자동으로 인출 다른 활성 IPsec 터널 합니다. Azure 측 hello hello 스위치를 통해 영향을 받는 hello 인스턴스 toohello 활성 인스턴스를 자동으로 수행 됩니다.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>이중 중복: Azure와 온-프레미스 네트워크에 대한 활성-활성 VPN Gateway
hello 가장 안정적인 방법은 네트워크와 Azure 모두 toocombine hello 액티브-액티브 게이트웨이 아래 hello 다이어그램에 나와 있는 것 처럼입니다.

![이중 중복](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

여기 만들고는 활성-활성 구성의 hello Azure VPN 게이트웨이 설치 합니다. 한 두 개의 로컬 네트워크 게이트웨이 만들기 및 사용자 2에 대 한 두 개의 연결 온-프레미스 VPN 장치 위에서 설명한 것 처럼 합니다. hello 결과 Azure 가상 네트워크와 온-프레미스 네트워크 간에 IPsec 터널 4의 풀 메시 연결입니다.

모든 게이트웨이 및 터널 hello Azure 측에서에서 활성, hello 트래픽을 갖게 됩니다 다시 수행 hello 동일한 터널 또는 경로에서 hello Azure 측 됩니다 사이 분산 모든 4 터널 동시에 각 TCP 또는 UDP 흐름 있지만 합니다. Hello 트래픽을 당겨 처리량이 약간 더 hello IPsec 터널을 통해 표시 될 수 있습니다, 없지만 고가용성을 위해이 구성의 기본 목표는 hello입니다. 있고 그것이 어려운 tooprovide hello 측정 toohello 통계 hello 확산에서는 이기 때문에 응용 프로그램 트래픽이 서로 어떻게 다른 지 조건에 영향을 줍니다 hello에 집계 처리량을 합니다.

이 토폴로지 두 로컬 네트워크 게이트웨이 및 온-프레미스 VPN 장치의 toosupport hello 쌍을 두 개의 연결이 필요 하 고 BGP 필요한 tooallow hello 두 연결 toohello는 동일한 온-프레미스 네트워크입니다. 이러한 요구 사항은 동일 hello로 hello [위에](#activeactiveonprem)합니다. 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Azure VPN Gateways를 통해 항상 사용 가능한 VNet 간 연결
hello 동일한 액티브-액티브 구성을 적용할 수도 tooAzure VNet 대 VNet 연결 합니다. 두 가상 네트워크에 대 한 액티브-액티브 VPN 게이트웨이 만들 수 있고 함께 tooform hello 전체 동일한 메시의 4 터널 hello 아래 다이어그램 hello와 같이 두 개의 Vnet 간의 연결에 연결 됩니다.

![VNet 간](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

이렇게 한 쌍의 hello 더 나은 가용성을 제공 하는 계획 된 유지 관리 이벤트에 대 한 두 개의 가상 네트워크 간의 터널 항상 됩니다. Hello 크로스-프레미스 연결에 대 한 토폴로지를 동일한 두 개의 연결이 필요, 경우에 위에 표시 된 hello VNet 대 VNet 토폴로지는 각 게이트웨이의 하나만 연결을 해야 합니다. 또한 hello VNet 대 VNet 연결을 통해 전송 라우팅과 필요 하지 않는 한 BGP 선택 사항입니다.

## <a name="next-steps"></a>다음 단계
참조 [크로스-프레미스 및 VNet 대 VNet 연결에 대해 액티브-액티브 VPN 게이트웨이 구성](vpn-gateway-activeactive-rm-powershell.md) 단계 tooconfigure 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 합니다.


---
title: "프레미스 간 연결을 위한 계획 및 설계: Azure VPN Gateway | Microsoft Docs"
description: "크로스-프레미스, 하이브리드, VNet 간 연결에 대한 VPN Gateway 계획 및 설계에 대해 알아보세요."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>VPN Gateway 계획 및 설계

크로스 프레미스 및 VNet-VNet 연결을 계획 및 설계할 경우 네트워킹 요구 사항에 따라 연결이 매우 단순하거나 복잡해질 수 있습니다. 이 문서에서는 계획 및 설계 시 기본적으로 고려해야 할 사항을 안내합니다.

## <a name="planning"></a>계획

### <a name="compare"></a>프레미스 간 연결 옵션

Tooconnect를 원하는 경우 온-프레미스 사이트 안전 하 게 tooa 가상 네트워크, 세 가지 방법으로 toodo 개일 있으므로: 사이트 간 및 지점-사이트 및 express 경로입니다. 사용할 수 있는 hello 다른 크로스-프레미스 연결을 비교 합니다. hello 옵션 선택와 같은 다양 한 고려 사항에 따라 달라질 수 있습니다.

* 솔루션에 어떤 종류의 처리량이 필요한가요?
* 시겠습니까 toocommunicate hello를 통해 공용 인터넷 또는 개인 연결을 보안 VPN을 통해?
* 공용 IP 주소 사용 가능한 toouse 있습니까?
* VPN 장치 toouse 계획 입니까? 그렇다면 해당 장치가 호환되나요?
* 컴퓨터 몇 대만 연결하시겠어요? 아니면 사이트에 대한 영구 연결을 원하세요?
* 어떤 유형의 VPN 게이트웨이 필요는 원하는 toocreate hello 솔루션에 대 한?
* 어떤 게이트웨이 SKU를 사용해야 합니까?

### <a name="planningtable"></a>계획 표

다음 표는 hello hello 솔루션에 대 한 최상의 연결 옵션을 결정 하는 데 유용 합니다.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>게이트웨이 SKU

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>워크플로

hello 다음 목록 윤곽선 hello 클라우드 연결에 대 한 일반적인 워크플로:

1. 디자인와 모든 네트워크에 대 한 연결 토폴로지 및 목록 hello 주소 공간 계획 tooconnect 호출 합니다.
2. Azure 가상 네트워크를 만듭니다. 
3. Hello 가상 네트워크용 VPN 게이트웨이 만듭니다.
4. 만들고 필요에 따라 tooon 온-프레미스 네트워크 연결 또는 다른 가상 네트워크를 구성 합니다.
5. 필요에 따라 Azure VPN Gateway에 대한 지점 및 사이트 간 연결을 만들고 구성합니다.

## <a name="design"></a>디자인
### <a name="topologies"></a>연결 토폴로지

Hello 다이어그램 hello에 확인 하 여 시작 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 문서. hello 문서 기본 다이어그램, 각 토폴로지와 hello 사용 가능한 배포 도구 구성 toodeploy를 사용할 수 있습니다에 대 한 hello 배포 모델을 포함 합니다.

### <a name="designbasics"></a>디자인 기본 사항

다음 섹션 hello hello VPN 게이트웨이 기본 사항에 설명 합니다. 

#### <a name="servicelimits"></a>네트워킹 서비스 제한

Hello 테이블 tooview 통해 스크롤 [네트워킹 서비스 제한](../azure-subscription-service-limits.md#networking-limits)합니다. 나열 된 hello 제한 디자인에 영향을 줄 수 있습니다.

#### <a name="subnets"></a>서브넷 정보

연결을 만들 때 서브넷 범위를 고려해야 합니다. 서브넷 주소 범위가 겹치면 안 됩니다. 다른 위치를 hello 같은 주소 공간을 포함 하는 hello 한 가상 네트워크 또는 온-프레미스 위치가 포함 되어 있으면에 겹치는 서브넷. 즉, Azure IP에 대 한 사용자 로컬 온-프레미스 네트워크 toocarve toouse 있습니다에 대 한 기간에 네트워크 엔지니어를 필요한 공간/서브넷 주소를 지정 합니다. Hello 로컬 온-프레미스 네트워크에서 사용 되지 않는 주소 공간이 필요 합니다.

또한 VNet 간 연결을 사용할 때는 서브넷이 중복되지 않도록 하는 것이 중요합니다. 서브넷 겹치는 IP 주소에 있는 경우 hello 보내기 및 대상 Vnet VNet 대 VNet 연결 실패 합니다. Azure는 hello 대상 주소 hello VNet 전송의 일부 이므로 hello 데이터 toohello 다른 VNet 라우팅할 수 없습니다.

VPN Gateway에는 게이트웨이 서브넷이라는 특정 서브넷이 필요합니다. 모든 게이트웨이 서브넷 이름을 지정 해야 GatewaySubnet toowork 제대로 합니다. 확인 되지 tooname 다른 게이트웨이 서브넷 이름을 지정 하 고 Vm 또는 다른 무엇 toohello 게이트웨이 서브넷에 배포 하지는 않습니다. [게이트웨이 서브넷](vpn-gateway-about-vpn-gateway-settings.md#gwsub)을 참조하세요.

#### <a name="local"></a>로컬 네트워크 게이트웨이 정보

일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다. Hello 클래식 배포 모델 hello 로컬 네트워크 게이트웨이 로컬 네트워크 사이트 참조 tooas 합니다. 로컬 네트워크 게이트웨이 구성할 때 이름을 지정, hello hello 온-프레미스 VPN 장치의 공용 IP 주소를 지정 했으며 hello 온-프레미스 위치에 있는 hello 주소 접두사를 지정 합니다. Azure는 네트워크 트래픽에 대 한 hello 대상 주소 접두사에 조회 하 고, 사용자가 지정한 hello 구성 hello 로컬 네트워크 게이트웨이에 대 한 참조, 그에 따라 패킷을 라우팅할 합니다. 필요에 따라 hello 주소 접두사를 수정할 수 있습니다. 자세한 내용은 [로컬 네트워크 게이트웨이](vpn-gateway-about-vpn-gateway-settings.md#lng)를 참조하세요.

#### <a name="gwtype"></a>게이트웨이 형식 정보

토폴로지에 대 한 hello 올바른 게이트웨이 유형을 선택 하는 것이 중요 합니다. Hello 잘못 된 유형을 선택 하면 게이트웨이가 제대로 작동 하지 않습니다. hello 게이트웨이 유형을 hello 게이트웨이 자체 연결 하 고 hello 리소스 관리자 배포 모델에 대 한 필수 구성 설정 하는 방법을 지정 합니다.

hello 게이트웨이 유형은 다음과 같습니다.

* Vpn
* Express 경로

#### <a name="connectiontype"></a>연결 형식 정보

각 구성이 작동하려면 특정 연결 형식이 필요합니다. hello 연결 유형은 다음과 같습니다.

* IPsec
* Vnet2Vnet
* Express 경로
* VPNClient

#### <a name="vpntype"></a>VPN 형식 정보

각 구성에는 특정 VPN 형식이 필요합니다. 사이트 간 연결과 지점 및 사이트 연결 toohello 만들기와 같은 두 가지 구성을 결합 하는 경우 동일한 VNet 연결 요구 사항을 모두 충족 하는 VPN 형식을 사용 해야 합니다.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

hello 다음 표에서 보여 hello VPN 유형을 대로 tooeach 연결 구성에 매핑합니다. 있는지 hello toocreate 원하는 게이트웨이 일치 hello 구성에 대 한 VPN 유형을 확인 하십시오. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>사이트 간 연결에 대한 VPN 장치

사이트-사이트 tooconfigure 연결 배포 모델에 관계 없이 다음 항목 hello가 필요 합니다.

* Azure VPN Gateway와 호환되는 VPN 장치
* NAT 뒤에 있지 않은 공용 IPv4 IP 주소

VPN 장치를 구성 하는 toohave 경험 필요 또는 누군가가 수 있는 hello 장치를 구성 합니다.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>강제 터널 라우팅 고려

대부분의 구성에서 강제 터널링을 구성할 수 있습니다. 강제 터널링 리디렉션 또는 "강제" 검사 및 감사용 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치로 사용 하면 됩니다. 대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다. 

강제 터널링 기능이 없으면 Azure 내 Vm의에서 인터넷 바인딩된 트래픽이 항상 트래버스할 hello 옵션 tooallow 없이 toohello 인터넷 아웃 직접 Azure 네트워크 인프라에서 있습니다 tooinspect 또는 감사 hello 트래픽을 합니다. 인터넷에 대 한 무단된 액세스 tooinformation 노출 또는 기타 유형의 보안 위반을 일으킬 수 있습니다.

두 배포 모델에서 다양한 도구를 사용하여 강제 터널링 연결을 구성할 수 있습니다. 자세한 내용은 [강제 터널링 구성](vpn-gateway-forced-tunneling-rm.md)을 참조하세요.

**강제 터널링 다이어그램**

![Azure VPN Gateway 강제 터널링 다이어그램](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>다음 단계

Hello 참조 [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md) 및 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md) 에 대 한 자세한 내용은 toohelp 있습니다으로 설정 된 아티클에 디자인 합니다.

특정 게이트웨이 설정에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.
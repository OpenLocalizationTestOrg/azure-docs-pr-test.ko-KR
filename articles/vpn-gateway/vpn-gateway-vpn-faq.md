---
title: "aaaAzure VPN 게이트웨이 FAQ | Microsoft Docs"
description: "hello VPN 게이트웨이 FAQ입니다. Microsoft Azure Virtual Network 프레미스 간 연결, 하이브리드 구성 연결 및 VPN Gateway에 대한 FAQ입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>VPN Gateway FAQ

## <a name="connecting"></a>Toovirtual 네트워크 연결

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>다양한 Azure 지역에서 가상 네트워크를 연결할 수 있습니까?

예. 실제로 지역 제약 조건이 없습니다. 하나의 가상 네트워크에 hello tooanother 가상 네트워크에 연결할 수 동일한 지역 또는 다른 Azure 지역에 있습니다. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>다른 구독의 가상 네트워크를 연결할 수 있습니까?

예.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>단일 가상 네트워크에서 toomultiple 사이트를 연결할 수 있습니까?

Windows PowerShell 및 hello Azure REST Api를 사용 하 여 toomultiple 사이트에 연결할 수 있습니다. Hello 참조 [다중 사이트 및 VNet 대 VNet 연결](#V2VMulti) FAQ 섹션.

### <a name="what-are-my-cross-premises-connection-options"></a>내 프레미스 간 연결 옵션은 무엇입니까?

다음 hello 크로스-프레미스 연결이 지원 됩니다.

* 사이트 간 – IPsec 통한 VPN 연결(IKE v1 및 IKE v2). 이 연결 유형은 VPN 장치 또는 RRAS가 필요합니다. 자세한 내용은 [사이트 간](vpn-gateway-howto-site-to-site-resource-manager-portal.md)을 참조하세요.
* 지점 및 사이트 간 -SSTP를 통한 VPN 연결(보안 소켓 터널링 프로토콜). 이 연결에는 VPN 장치가 필요하지 않습니다. 자세한 내용은 [지점 및 사이트 간](vpn-gateway-howto-point-to-site-resource-manager-portal.md)을 참조하세요.
* VNet 대 VNet-이러한 유형의 연결은 사이트 간 구성과 동일 hello 됩니다. VNet tooVNet IPsec (IKE v1 및 IKE v2)을 통한 VPN 연결입니다. VPN 장치가 필요하지 않습니다. 자세한 내용은 [VNet 간](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)을 참조하세요.
* 다중 사이트-이 tooconnect 수 있는 사이트 간 구성의 한 종류로 여러 온-프레미스 사이트 tooa 가상 네트워크입니다. 자세한 내용은 [다중 사이트](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)를 참조하세요.
* Express 경로 – ExpressRoute는 WAN 통해 hello VPN 연결이 아닌에서 직접 연결 tooAzure 공용 인터넷 합니다. 자세한 내용은 참조 hello [express 경로 기술 개요](../expressroute/expressroute-introduction.md) 및 hello [express 경로 FAQ](../expressroute/expressroute-faqs.md)합니다.

VPN Gateway 연결에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>사이트 간 연결과 지점 및 사이트 간에 hello 차이점은 무엇입니까?

**사이트 간**(IPsec/IKE VPN 터널) 구성은 온-프레미스 위치와 Azure 사이에 있습니다. 즉, 온 프레미스 tooany 가상 컴퓨터나 역할 인스턴스 tooconfigure 라우팅 및 권한을 선택 하는 방법에 따라 가상 네트워크 내에 있는 컴퓨터의에서 연결할 수 있습니다. 이 연결은 항상 사용할 수 있는 프레미스 간 연결에 유용한 옵션이며 하이브리드 구성에 적합합니다. 이러한 종류의 연결 hello 경계 네트워크에 배포 되어야 IPsec VPN 어플라이언스 (하드웨어 장치 또는 소프트 어플라이언스)에 의존 합니다. toocreate 이러한 종류의 연결 있어야 NAT 뒤에 있지 않는 한 외부와 접한 IPv4 주소

**지점 및 사이트** (SSTP VPN) 구성을 tooanything 가상 네트워크에 있는 모든 위치에서 단일 컴퓨터에서 연결 하는 데 사용 합니다. Hello Windows 기본 VPN 클라이언트를 사용합니다. Hello 지점-사이트 구성의 일부로 인증서와 컴퓨터 tooconnect tooany 가상 컴퓨터나 역할 인스턴스 hello 가상 네트워크 내에서 허용 하는 hello 설정을 포함 하는 VPN 클라이언트 구성 패키지를 설치 합니다. 온-프레미스 아닌 tooconnect tooa 가상 네트워크를 사용할 때 유용 합니다. 액세스 tooVPN 하드웨어 또는 외부와 접한 IPv4 주소는 모두 해당 하는 사이트 간 연결에 필요한 수 없을 때 적합 한 옵션 이기도 합니다.

두 사이트 및 사이트 간 가상 네트워크 toouse를 구성할 수 있습니다 및 지점 및 사이트 간 동시에 경로 기반 VPN을 사용 하 여 사이트 간 연결을 만드는 것 만큼 오래 게이트웨이에 대 한 입력 합니다. 경로 기반 VPN 유형 hello 클래식 배포 모델에서 동적 게이트웨이 라고 합니다.

## <a name="gateways"></a>가상 네트워크 게이트웨이

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>VPN Gateway는 가상 네트워크 게이트웨이인가요?

VPN Gateway는 가상 네트워크 게이트웨이의 유형입니다. VPN Gateway는 공용 연결을 통해 가상 네트워크와 온-프레미스 위치 간에 암호화된 트래픽을 전송합니다. 또한 가상 네트워크 간의 VPN 게이트웨이 toosend 트래픽을 사용할 수 있습니다. VPN 게이트웨이 만들 때 hello-GatewayType 값 'Vpn'를 사용 합니다. 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.

### <a name="what-is-a-policy-based-static-routing-gateway"></a>정책 기반(고적 라우팅) 게이트웨이란?

정책 기반 게이트웨이는 정책 기반 VPN을 구현합니다. 정책 기반 Vpn을 암호화 하 고 온-프레미스 네트워크 및 hello Azure VNet 간의 주소 접두사의 hello 조합에 따라 IPsec 터널을 통해 패킷을 합니다. hello 정책 (또는 트래픽 선택기)은 일반적으로 hello VPN 구성에 대 한 액세스 목록으로 정의 됩니다.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>경로 기반(동적 라우팅) 게이트웨이란?

경로 기반 게이트웨이 구현 hello 경로 기반 Vpn. 경로 기반 Vpn hello ip 전달 또는 해당 터널 인터페이스에 테이블 toodirect 패킷을 라우팅하려면 "라우팅"를 사용 합니다. hello 터널 인터페이스 다음 암호화 또는 hello 패킷에 hello 터널 내부 및 외부 암호를 해독 합니다. 경로 기반 Vpn으로 any-에-모든 구성에 대 한 정책 또는 트래픽 선택기 hello (또는 와일드 카드).

### <a name="do-i-need-a-gatewaysubnet"></a>'GatewaySubnet'이 필요한가요?

예. hello 게이트웨이 서브넷 hello 가상 네트워크 게이트웨이 서비스를 사용 하는 hello IP 주소를 포함 합니다. 가상 네트워크 게이트웨이 순서 tooconfigure에 VNet 게이트웨이 서브넷 toocreate가 필요합니다. 모든 게이트웨이 서브넷 이름을 지정 해야 'GatewaySubnet' toowork 제대로 합니다. 게이트웨이 서브넷에 다른 이름을 지정하지 않습니다. 및 Vm 또는 다른 무엇 toohello 게이트웨이 서브넷에 배포 하지는 않습니다.

Hello 게이트웨이 서브넷을 만들 때 포함 하는 hello 수가 IP 주소 서브넷 hello를 지정할 수 있습니다. hello 게이트웨이 서브넷의 IP 주소가 hello toohello 게이트웨이 서비스에 할당 됩니다. 일부 구성 더 많은 IP 주소 toobe 할당 toohello 게이트웨이 서비스 다른 사용자 보다 필요 합니다. 게이트웨이 서브넷에 충분 한 IP 주소 tooaccommodate 향후 성장 및 가능한 추가 새 연결 구성을 포함 되어 있는지 toomake 사용 하는 것이 좋습니다. 따라서 게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 게이트웨이 서브넷을 /27 이상으로 만드는 것이 좋습니다(/27, /26, /25 등). Toocreate 원하고 있는 hello 게이트웨이 서브넷 이러한 요구 사항을 충족 확인 hello 구성에 대 한 hello 요구 사항을 확인 합니다.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>가상 컴퓨터 또는 역할 인스턴스 toomy 게이트웨이 서브넷을 배포할 수 있습니까?

아니요.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>VPN 게이트웨이 IP 주소를 만들기 전에 내 VPN 게이트웨이 IP 주소를 가져올 수 있나요?

아니요. Toocreate 게이트웨이 첫 번째 tooget hello IP 주소를 해야 합니다. hello IP 주소 변경 내용을 삭제 하 고 VPN 게이트웨이 다시 만듭니다.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>VPN Gateway에 고정 공용 IP 주소를 요청할 수 있나요?

아니요. 동적 IP 주소 할당만 지원됩니다. 그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에이 아닙니다. hello 유일한 시간 hello VPN 게이트웨이 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다. 크기 조정, 다시 설정, 또는 기타 내부 유지 관리/업그레이드 VPN 게이트웨이의 hello VPN 게이트웨이 공용 IP 주소가 변경 되지 않습니다. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>내 VPN 터널을 어떻게 인증합니까?

Azure VPN은 PSK(미리 공유한 키) 인증을 사용합니다. Hello VPN 터널 만들 때 (PSK) 미리 공유한 키를 생성 합니다. Hello 자동 생성 된 PSK tooyour hello 사전 공유 키 설정 PowerShell cmdlet 또는 REST API를 직접 변경할 수 있습니다.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>사용할 수 있습니까 hello 사전 공유 키 API 설정 tooconfigure 내 정책 기반 (정적 라우팅) 게이트웨이 VPN?

예, hello 사전 공유 키 API 설정 및 PowerShell cmdlet 사용된 tooconfigure 수 Azure 정책 기반 (정적) Vpn 및 경로 기반 동적 라우팅 Vpn은 모두입니다.

### <a name="can-i-use-other-authentication-options"></a>다른 인증 옵션을 사용할 수 있습니까?

제한 된 toousing 사전 공유 키 인증을 위해 만든 PSK ()는입니다.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>지정 하는 방법는 트래픽이 hello VPN 게이트웨이 통과?

#### <a name="resource-manager-deployment-model"></a>리소스 관리자 배포 모델

* PowerShell: hello 로컬 네트워크 게이트웨이에 대 한 "AddressPrefix" toospecify 트래픽을 사용 합니다.
* Azure 포털: 탐색 toohello 로컬 네트워크 게이트웨이 > 구성 > 주소 공간입니다.

#### <a name="classic-deployment-model"></a>클래식 배포 모델

* Azure 포털: toohello 클래식 가상 네트워크를 이동 > VPN 연결 > 사이트 간 VPN 연결 > 로컬 사이트 이름 > 로컬 사이트 > 클라이언트 주소 공간입니다. 
* 클래식 포털: 각 범위에 사용 하려는 hello 게이트웨이 통해 보낸 hello 네트워크 페이지에서 로컬 네트워크에 가상 네트워크를 추가 합니다. 

### <a name="can-i-configure-forced-tunneling"></a>강제 터널링을 구성할 수 있습니까?

예. [강제 터널링 구성](vpn-gateway-about-forced-tunneling.md)을 참조하세요.

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>Azure에서 내 VPN 서버를 설정 및 tooconnect toomy 온-프레미스 네트워크를 사용할 수 있습니까?

예, 사용자 고유의 VPN 게이트웨이 또는 hello Azure 마켓플레이스 또는 사용자 고유의 VPN 라우터 만들기에서 Azure의 서버를 배포할 수 있습니다. 사용자 정의 경로 tooconfigure 필요한 가상 네트워크의 tooensure 트래픽이 적절히 라우터 온-프레미스 네트워크와 가상 네트워크 서브넷 간의 합니다.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>내 VPN 게이트웨이에서 특정 포트가 열리는 이유는 무엇인가요?

Azure 인프라 통신을 위해 필요합니다. Azure 인증서에 의해 보호(잠김)됩니다. 적절 한 인증서가 없는 외부 엔터티를 해당 게이트웨이 hello 고객을 포함 하 여 수 toocause 모든 해당 끝점에 적용 되지 않습니다.

VPN 게이트웨이 다중 홈 장치가 hello 고객 개인 네트워크 1 개 그리고 NIC 연결 hello 공용 네트워크에 관여 하는 NIC 1 개를 기본적으로 합니다. Azure 인프라 엔터티 하므로, tooutilize 공용 끝점 인프라 통신에 대 한 규정 준수 상의 이유로 고객 개인 네트워크를 활용할 수 없습니다. 공용 끝점 hello Azure 보안 감사에 의해 정기적으로 검색 됩니다.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>게이트웨이 유형, 요구 사항 및 처리량에 대한 자세한 내용

자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.

## <a name="s2s"></a>사이트 간 연결 및 VPN 장치

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>VPN 장치를 선택할 때 고려할 사항은 무엇입니까?

장치 공급업체와 협력하여 표준 사이트 간 VPN 장치의 유효성을 검사했습니다. 알려진된 호환 VPN 장치, 구성 하는 지침 또는 샘플 및 장치 사양 목록은 hello에 있습니다 [에 대 한 VPN 장치](vpn-gateway-about-vpn-devices.md) 문서. 알려진된 호환으로 표시 하는 hello 장치 제품군의 모든 장치는 가상 네트워크와 함께 작동 해야 합니다. toohelp은 VPN 장치를 구성 하려면이 toohello 장치 구성 샘플 또는 tooappropriate 장치 제품군을 해당 하는 링크를 참조 하십시오.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>VPN 장치 구성 설정을 어디서 찾을 수 있나요?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>VPN 장치 구성 샘플을 편집하려면 어떻게 하나요?

장치 구성 샘플을 편집하는 방법에 대한 정보는 [샘플 편집](vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>IPsec 및 IKE 매개 변수를 어디서 찾을 수 있나요?

IPsec/IKE 매개 변수는 [매개 변수](vpn-gateway-about-vpn-devices.md#ipsec)를 참조하세요.

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>트래픽이 유휴 상태일 때 정책 기반 VPN 터널이 다운되는 이유는 무엇인가요?

정책 기반(정적 라우팅이라고도 함) VPN 게이트웨이에서 예상되는 동작입니다. 5 분 이상 hello 트래픽 hello 터널을 통해 유휴 상태 이면 hello 터널 종료 될 됩니다. 트래픽 흐름 어느 방향에 시작 되 면 즉시 hello 터널 다시 설정 됩니다.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>소프트웨어 Vpn tooconnect tooAzure를 사용할 수 있습니까?

사이트 사이 프레미스 간 구성에 대해 Windows Server 2012 RRAS(라우팅 및 원격 액세스) 서버를 지원합니다.

으로 tooindustry 표준 IPsec 구현을 따르는 다른 소프트웨어 VPN 솔루션은 우리의 게이트웨이에서 작동 해야 합니다. 구성 및 지원 지침에 대 한 hello hello 소프트웨어 공급 업체에 문의 합니다.

## <a name="P2S"></a>지점 및 사이트 간 연결

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>VNet 간 연결 및 다중 사이트 연결

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>내 온-프레미스 사이트 또는 tooanother 가상 네트워크 간의 Azure VPN 게이트웨이 tootransit 트래픽을 사용할 수 있습니까?

**리소스 관리자 배포 모델**<br>
예. Hello 참조 [BGP](#bgp) 한 자세 합니다.

**클래식 배포 모델**<br>
Azure VPN 게이트웨이 통한 트래픽 전송은 hello 클래식 배포 모델을 사용 하 여 하지만 hello 네트워크 구성 파일에서 정적으로 정의 된 주소 공간에 의존 합니다. BGP은 hello 클래식 배포 모델을 사용 하 여 Azure 가상 네트워크 및 VPN 게이트웨이를 아직 지원 되지 않습니다. BGP를 사용하지 않고 전송 주소 공간을 수동으로 정의하면 오류가 발생하기 쉬우므로 사용하지 않는 것이 좋습니다.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure 생성 hello 동일한 IPsec/IKE 사전 공유 키 hello에 대 한 모든 VPN 연결에 대 한 동일 가상 네트워크?

아니요, 기본적으로 Azure는 VPN 연결마다 다른 미리 공유한 키를 생성합니다. 그러나 hello 설정 VPN 게이트웨이 키 REST API 또는 PowerShell cmdlet tooset hello 원하는 키 값을 사용할 수 있습니다. hello 키는 1 too128 자 사이의 영숫자가 문자열 이어야 합니다.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>단일 가상 네트워크보다 더 많은 사이트 간 VPN을 사용하면 대역폭이 증가합니까?

아니요. 지점-사이트 Vpn을 비롯 한 모든 VPN 터널을 공유 동일한 Azure VPN 게이트웨이 및 hello 사용 가능한 대역폭 hello 합니다.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>다중 사이트 VPN을 사용하여 내 가상 네트워크와 온-프레미스 사이트 간에 여러 터널을 구성할 수 있습니까?

예, 두 터널 toohello에서 BGP를 구성 해야 하지만 동일한 위치입니다.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>여러 VPN 터널을 포함하는 내 가상 네트워크에서 지점 및 사이트 간 VPN을 사용할 수 있습니까?

예, toomultiple 온-프레미스 사이트와 다른 가상 네트워크를 연결 하는 hello VPN 게이트웨이 사용 지점 및 사이트 간 (P2S) Vpn은 사용할 수 있습니다.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>IPsec Vpn toomy ExpressRoute 회로와 가상 네트워크를 연결할 수 있습니까?

예, 지원됩니다. 자세한 내용은 [공존하는 ExpressRoute 및 사이트 간 VPN 연결 구성](../expressroute/expressroute-howto-coexist-classic.md)을 참조하세요.

## <a name="ipsecike"></a>IPsec/IKE 정책

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>크로스-프레미스 연결 및 VM

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>내 가상 컴퓨터는 가상 네트워크에 크로스-프레미스 연결을 해야 연결 어떻게 toohello VM?

몇 가지 옵션이 있습니다. VM에 대해 활성화 RDP를 설정한 경우에 hello 개인 IP 주소를 사용 하 여 tooyour 가상 컴퓨터를 연결할 수 있습니다. 이 경우 hello 개인 IP 주소와 hello 원하는 포트를 tooconnect 너무 (일반적으로 3389)을 지정 합니다. Tooconfigure hello 포트 hello 트래픽에 대 한 가상 컴퓨터에 필요 합니다.

찾았으며 hello에 동일한 다른 가상 컴퓨터에서 개인 IP 주소 여 tooyour 가상 컴퓨터를 연결할 수도 있습니다 가상 네트워크입니다. 가상 네트워크 외부 위치에서 연결 하는 경우에 hello 개인 IP 주소를 사용 하 여 RDP tooyour 가상 컴퓨터 수는 없습니다. 예를 들어 지점 및 사이트 간 가상 네트워크 구성 있고 사용자 컴퓨터에서 연결을 설정 하지 않는 경우 toohello 가상 컴퓨터 개인 IP 주소를 통해 연결할 수 없습니다.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>내 가상 컴퓨터가 크로스-프레미스 연결을 사용 하 여 가상 네트워크에 있는 경우 내 VM의 모든 hello 트래픽이 통과 않으므로 해당 연결?

아니요. 대상이 hello 트래픽만 hello 가상 네트워크 게이트웨이 통해 사용자가 지정한 hello 가상 네트워크 로컬 네트워크 IP 주소 범위에 포함 된 IP 전환 됩니다. 트래픽은 hello 가상 네트워크 내에 있는 IP hello 가상 네트워크 내부에 머무는 대상을 있습니다. 다른 트래픽은 hello 부하 분산 장치 toohello 공용 네트워크를 통해 전송 되었거나 hello Azure VPN 게이트웨이 통해 강제 터널링을 사용 하는 경우 전송 됩니다.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>RDP 연결 tooa VM을 해결 하려면 어떻게 해야 합니까

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Virtual Network FAQ

Hello에서 추가 가상 네트워크 정보를 볼 [가상 네트워크 FAQ](../virtual-network/virtual-networks-faq.md)합니다.

## <a name="next-steps"></a>다음 단계

* VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.
* VPN Gateway 구성 설정에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.

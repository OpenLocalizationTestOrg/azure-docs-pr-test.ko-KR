---
title: "aaaNetwork 보안 개념 및 Azure에서 요구 사항 | Microsoft Docs"
description: " 이 문서 쉽게 있습니다 toounderstand 어떤 Microsoft Azure hello 네트워크 보안 영역에 대 한 toooffer 합니다. 핵심 네트워크 보안 개념 및 요구 사항에 대 한 기본적인 설명을 제공 많고는 Azure에 대 한 정보 toooffer의 각이 영역입니다. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Azure 네트워크 보안 개요
Microsoft Azure 응용 프로그램 및 서비스 연결 요구 사항 강력한 네트워킹 인프라 toosupport를 포함합니다. Azure 호스팅 리소스 및 hello 인터넷에서에서 tooand 및 Azure 있으며 온-프레미스 간에 Azure에 배치 된 리소스 간에 네트워크 연결 됩니다.

이 문서의 hello 목표는 toomake 있습니다 toounderstand 손쉽게 어떤 Microsoft Azure에 toooffer의 hello 영역에서 네트워크 보안 합니다. 여기서 핵심 네트워크 보안 개념 및 요구 사항에 대한 기본적인 설명을 제공할 뿐만 아니라 Azure에 정보 toooffer를 각이 영역에 뿐만 아니라 관심 있는 영역에 대 한 깊은 이해가 얻을 toohelp 연결도 제공 합니다.

이 Azure 네트워크 보안 개요 문서 hello 영역을 다음에 중점을 둡니다.

* Azure 네트워킹
* 네트워크 액세스 제어
* 안전한 원격 액세스 및 크로스-프레미스 연결
* Availability
* 이름 확인
* DMZ 아키텍처
* 감사 및 위협 검색


## <a name="azure-networking"></a>Azure 네트워킹
가상 컴퓨터는 네트워크 연결이 필요합니다. toosupport 해당 요구 사항을 Azure 필요 연결 된 가상 컴퓨터 toobe tooan Azure 가상 네트워크입니다. Azure 가상 네트워크는 hello Azure 실제 네트워크 패브릭 기반으로 하는 논리적 구문입니다. 각 논리적 Azure Virtual Network는 다른 모든 Azure Virtual Network와 격리됩니다. 이렇게 하면 네트워크 트래픽 양 배포에 액세스할 수 있는 tooother Microsoft Azure 고객과 아닌지 확인 합니다.

자세한 정보:

* [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>네트워크 액세스 제어
네트워크 액세스 컨트롤은 특정 장치 또는 Azure 가상 네트워크 내의 서브넷에서 연결 tooand 제한 hello 해야입니다. 네트워크 액세스 제어의 hello 목표는 toolimit 액세스 tooyour 가상 컴퓨터 및 서비스 tooapproved 사용자 및 장치입니다. 액세스 제어를 기반으로 허용 하거나 가상 컴퓨터 또는 서비스에서 연결 tooand에 대 한 결정을 거부 합니다.

Azure는 다음과 같은 다양한 유형의 네트워크 액세스 제어를 지원합니다.

* 네트워크 계층 제어
* 경로 제어 및 터널링 적용
* 가상 네트워크 보안 어플라이언스

### <a name="network-layer-control"></a>네트워크 계층 제어
모든 보안 배포에는 몇 가지 네트워크 액세스 제어가 필요합니다. hello 네트워크 액세스 제어의 ´ ֲ toorestrict 가상 컴퓨터 통신 toohello 필요한 시스템 및 다른 통신 시도 차단 됩니다.

기본 네트워크 수준 액세스 제어 (IP 주소와 hello TCP 또는 UDP 프로토콜에 따라) 해야 할 경우 네트워크 보안 그룹을 사용할 수 있습니다. 보안 그룹 NSG (네트워크)은 기본 상태 저장 패킷 필터링 방화벽 toocontrol 액세스할 수에 따라 수 있으며 한 [5-튜플](https://www.techopedia.com/definition/28190/5-tuple)합니다. NSG는 응용 프로그램 계층 검사 또는 인증된 액세스 제어를 제공하지 않습니다.

자세한 정보:

* [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>경로 제어 및 터널링 적용
Azure 가상 네트워크에 hello 기능 toocontrol 라우팅 동작 중요 한 네트워크 보안 및 액세스 제어 기능입니다. 라우팅 잘못 구성 된, 응용 프로그램 및 가상 컴퓨터에서 호스팅되는 서비스 소유 및 잠재적 공격자가 운영 체제를 포함 하 여 toounauthorized 장치에 연결할 수 있습니다.

Azure 네트워킹은 Azure 가상 네트워크에서 네트워크 트래픽에 대 한 hello 기능 toocustomize hello 라우팅 동작을 지원 합니다. 이렇게 하면 Azure 가상 네트워크의 tooalter hello 기본 라우팅 테이블 항목입니다. 라우팅 동작을 제어하면 특정 장치 또는 장치 그룹의 모든 트래픽이 특정 위치를 통해 가상 네트워크에 진입하거나 떠납니다.

예를 들어, Azure 가상 네트워크에 가상 네트워크 보안 어플라이언스가 있을 수 있습니다. Azure 가상 네트워크에서 모든 트래픽 tooand 해당 가상 보안 어플라이언스 거치 있는지 toomake 사용 하는 것이 좋습니다. Azure에서 [사용자 정의 경로](../virtual-network/virtual-networks-udr-overview.md)를 구성하면 이 작업을 수행할 수 있습니다.

[강제 터널링](https://www.petri.com/azure-forced-tunneling) tooensure 없는 서비스를 사용할 수 있는 메커니즘에 사용할 수 tooinitiate 연결 toodevices hello 인터넷 합니다. 이 들어오는 연결을 수락 하 고 응답 한 다음 다른 toothem 합니다. 프런트 엔드 웹 서버 인터넷 호스트에서 toorespond toorequests 하며 toorespond 인바운드 toothese 웹 서버와 웹 서버 hello 수 인터넷 원본에서 얻었는지 트래픽이 허용 됩니다.

어떤 않으려면 tooallow은 프런트 엔드 웹 서버 tooinitiate 아웃 바운드 요청 해야 합니다. 이러한 연결에 사용 되는 toodownload 맬웨어 일 수 있으므로 이러한 요청 보안 위험을 나타낼 수 있습니다. 도 않을 경우 이러한 프런트 엔드 서버 tooinitiate 아웃 바운드를 요청 하는 인터넷 toohello tooforce 할 수 있습니다 이러한 toogo 온-프레미스를 통해 웹 프록시 URL 필터링 및 로깅의 이용할 수 있도록 합니다.

대신, toouse 강제 터널링 tooprevent이 사용할 수 있습니다. 강제 터널링을 사용 하면 온-프레미스 게이트웨이 통해 모든 연결 toohello 인터넷 강제 합니다. 사용자 정의 경로를 활용하여 터널링 적용을 구성할 수 있습니다.

자세한 정보:

* [사용자 정의된 경로 및 IP 전달이란?](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>가상 네트워크 보안 어플라이언스
네트워크 보안 그룹, 사용자 정의 경로 및 강제 터널링 제공 hello의 hello 네트워크와 전송 계층에서 보안 수준의 [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 더 높은 수준에서 tooenable 보안 할 때가 있을 수 있습니다 보다 hello 네트워크입니다.

예를 들어, 다음과 같은 보안 요구 사항이 있을 수 있습니다.

* 인증 및 권한 부여 tooyour 응용 프로그램 액세스를 허용 하기 전에
* 침입 감지 및 침입 대응
* 높은 수준의 프로토콜에 대한 응용 프로그램 계층 검사
* URL 필터링
* 네트워크 수준 바이러스 백신 및 맬웨어 방지
* 안티봇 보호
* 응용 프로그램 액세스 제어
* Hello DDoS 제공 보호 hello 자체 Azure 패브릭이) (위 추가 DDoS 보호

Azure 파트너 솔루션을 사용하여 이러한 향상된 네트워크 보안 기능에 액세스할 수 있습니다. Hello를 방문 하 여 hello 최신 Azure 파트너 네트워크 보안 솔루션을 찾을 수 있습니다 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) "보안" 및 "네트워크 보안 합니다."를 검색 하 고

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>안전한 원격 액세스 및 크로스-프레미스 연결
설치, 구성 및 Azure 리소스 관리 toobe 원격으로 수행 해야 합니다. 또한 toodeploy 경우가 [하이브리드 IT](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) 구성 요소가 온-프레미스를 포함 하는 솔루션 및 Azure 공용 클라우드에서 hello 합니다. 이러한 시나리오에는 보안 원격 액세스가 필요합니다.

Azure 네트워킹 hello 다음 보안 된 원격 액세스 시나리오를 지원 합니다.

* 개별 워크스테이션 tooan Azure 가상 네트워크를 연결 합니다.
* 온-프레미스 네트워크 tooan Azure 가상 네트워크 vpn 연결
* 전용된 WAN 링크를 사용 하 여 온-프레미스 네트워크 tooan Azure 가상 네트워크 연결
* 다른 Azure 가상 네트워크 tooeach 연결

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>개별 워크스테이션 tooan Azure 가상 네트워크를 연결 합니다.
시간을 tooenable 개별 개발자 또는 작업 담당자 toomanage 가상 컴퓨터 및 Azure 서비스에에서 있을 수 있습니다. 예를 들어 Azure 가상 네트워크에서 tooa 가상 컴퓨터에 액세스 해야 하 고 보안 정책에 RDP 또는 SSH 원격 액세스 tooindividual 가상 컴퓨터 허용 하지 않습니다. 이 경우에는 지점 및 사이트 간 VPN 연결을 사용할 수 있습니다.

지점 및 사이트 간 VPN 연결 사용 hello hello [SSTP VPN](https://technet.microsoft.com/library/cc731352.aspx) 프로토콜 tooenable hello 사용자와 hello Azure 가상 네트워크 간의 개인 및 보안 연결을 tooset 합니다. Hello VPN 연결이 설정 되 면 hello 사용자 수 tooRDP 됩니다 또는 SSH hello VPN 통해 hello (있는 hello 사용자를 인증할 수, 권한이 부여 되었는지) Azure 가상 네트워크의 가상 컴퓨터에 연결 합니다.

자세한 정보:

* [PowerShell을 사용 하 여 가상 네트워크는 지점 및 사이트 연결 tooa 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>온-프레미스 네트워크 tooan Azure 가상 네트워크 vpn 연결
전체 회사 네트워크 또는 일부를 Azure 가상 네트워크 tooan tooconnect 할 수 있습니다. 이것은 회사가 [온-프레미스 데이터 센터를 Azure로 확장](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84)하는 하이브리드 IT 시나리오에서 흔하게 일어나는 일입니다. 대부분 경우에 회사는 솔루션에 Azure의 프런트-엔드 웹 서버와 백-엔드 데이터베이스 온-프레미스를 포함하는 경우와 같이 Azure의 서비스 일부 또는 온-프레미스 일부를 호스팅합니다. 이러한 종류의 "크로스-프레미스" 연결은 Azure 위치 리소스를 더 안전하게 리하고 Active Directory 도메인 컨트롤러를 Azure로 확장하는 등의 시나리오를 활성화할 수 있게 줍니다.

한 가지 방법은 tooaccomplish toouse 이것이 [사이트 간 VPN](https://www.techopedia.com/definition/30747/site-to-site-vpn)합니다. 사이트 간 VPN과 지점-사이트 VPN의 hello 차이점은 지점-사이트 VPN 사이트 간 VPN은 전체 네트워크 (예: 온-프레미스 네트워크) tooan Azure 가상 네트워크를 연결 하는 동안 단일 장치 tooan Azure 가상 네트워크를 연결 . Azure 가상 네트워크 사이트 간 Vpn tooan hello 매우 안전한 IPsec 터널 모드 VPN 프로토콜을 사용 합니다.

자세한 정보:

* [리소스 관리자 VNet hello Azure 포털을 사용 하는 사이트 간 VPN 연결 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [VPN 게이트웨이 계획 및 설계](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>전용 WAN 링크를 사용 하 여 온-프레미스 네트워크 tooan Azure 가상 네트워크에 연결
지점 및 사이트 간과 사이트 간 VPN 연결은 크로스-프레미스 연결에 효과적입니다. 그러나 일부 조직에서는 고려해 toohave hello 다음 단점이 있습니다.

* Hello 인터넷을 통해 데이터를 이동 하는 VPN 연결-노출 되어 이러한 연결 toopotential 보안 문제 공용 네트워크를 통해 데이터를 이동 합니다. 또한, 인터넷 연결의 안정성 및 가용성을 보장할 수 없습니다.
* VPN 연결 tooAzure 가상 네트워크 대역폭 제한 일부 응용 프로그램 및 200 mbps max 때 목적으로 간주 될 수 있습니다.

일반적으로 가장 높은 수준의 보안 성능과 크로스-프레미스 연결에 대 한 가용성을 hello 해야 하는 조직은 전용된 WAN 링크 tooconnect tooremote 사이트를 사용 합니다. Azure 기능 toouse 사용할 수 있는 tooconnect 온-프레미스 네트워크 tooan Azure 가상 네트워크는 전용된 WAN 링크 hello를 제공 합니다. 이 작업은 Azure Express 경로를 통해 활성화됩니다.

자세한 정보:

* [Express 경로 기술 개요](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Azure 가상 네트워크 tooEach 연결 다른
Toouse 있습니다 수, 배포에 대 한 많은 Azure 가상 네트워크입니다. 이 작업이 가능한 여러 이유가 있습니다. Hello 이유 중 하나로 toosimplify 관리; 수 있습니다. 다른 보안상의 이유로 수도 있습니다. Hello 동기 또는 서로 다른 Azure 가상 네트워크에 배치 하는 리소스에 대 한 설명에 관계 없이 서로 hello 네트워크 tooconnect의 각 리소스 하려는 때 있을 수 있습니다.

"뒤로"를 반복 하 여 다른 Azure 가상 네트워크에서 Azure 가상 네트워크 tooconnect tooservices 하나에서 서비스에 대 한 한 가지 옵션 것 hello 인터넷을 통해. hello 연결 하나의 Azure 가상 네트워크에서 시작 하 고 hello 인터넷을 통해 이동 하 고에 다시 시도 toohello 대상 Azure 가상 네트워크 게 됩니다. 이 옵션 hello 연결 toohello 보안 문제 내재 된 tooany 인터넷 기반 통신을 제공합니다.

편이 더 나은지 toocreate는 Azure 가상 네트워크-Azure 가상 네트워크 사이트 간 VPN을 수 있습니다. 이 Azure 가상 네트워크-Azure 가상 네트워크 사이트 간 VPN 사용 하 여 hello 동일 [IPsec 터널 모드](https://technet.microsoft.com/library/cc786385.aspx) 위에서 언급 한 hello 크로스-프레미스 사이트 간 VPN 연결으로 프로토콜입니다.

Azure 가상 네트워크-Azure 가상 네트워크 사이트 간 VPN을 사용 하 여 hello 장점은 hello VPN 연결이 hello hello 인터넷을 통해 연결 하는 대신 Azure 네트워크 패브릭을 통해 설정 된입니다. 이 추가적인 보안 비교한 toosite-사이트 Vpn hello 인터넷을 통해 연결을 제공 합니다.

자세한 정보:

* [Azure Resource Manager 및 PowerShell을 사용하여 VNet-VNet 연결 구성](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Availability
가용성은 보안 프로그램의 핵심 구성 요소입니다. 사용자 및 시스템 효과 액세스할 수 없는 경우 필요한 tooaccess hello 통해 네트워크, hello 손상 서비스가 간주 될 수 있습니다. Azure에는 고가용성 메커니즘에 따라 해당 지원 hello 네트워킹 기술:

* HTTP 기반 부하 분산
* 네트워크 수준 부하 분산
* 전역 부하 분산

부하 분산은 메커니즘인 tooequally 여러 장치 간에 연결을 배포 합니다. 부하 분산의 목표 hello 같습니다.

* – 가용성을 높여 주는 여러 장치 간에 분산 연결을 로드 하 고 hello 장치 중 하나 이상이 있습니다 사용할 수 없게 hello 남은 온라인 장치에서 실행 하는 hello 서비스는 hello 서비스에서 tooserve hello 콘텐츠를 계속할 수 있습니다.
* 성능을 향상 시킬-단일 장치 tootake hello 프로세서 없는 여러 장치 간에 분산 연결을 로드할 때 적중 합니다. 대신, hello 처리 및 메모리 요구 hello 콘텐츠를 처리 하기 위한 여러 장치 간에 분배 됩니다.

### <a name="http-based-load-balancing"></a>HTTP 기반 부하 분산
적절 한 수준의 성능과 가용성을 보장 하는 웹 기반 서비스의 실행된 종종 toohave 해당 웹 서비스 toohelp 앞에 HTTP 기반 부하 분산 장치를 원하는 조직에서는 합니다. 반대로 tootraditional 네트워크 기반 부하 분산 장치, hello 부하 분산 결정에 의해 HTTP 기반 부하 분산 장치에서 특성을 기초로 hello 네트워크와 전송 계층 프로토콜에 없는 hello HTTP 프로토콜의 합니다.

tooprovide 있습니다 HTTP 기반 부하 분산-웹 기반 서비스에 대 한 Azure에서 Azure 응용 프로그램 게이트웨이 hello 제공 합니다. hello Azure 응용 프로그램 게이트웨이 지원:

* HTTP 기반 부하 분산-부하 분산을 결정 기준으로 특성 특수 toohello HTTP 프로토콜에서
* 쿠키 기반 세션 선호도-이 기능을 사용 하면 연결 설정 tooone 해당 부하 분산 장치 뒤에서 hello 서버 hello 클라이언트와 서버 간에 그대로 있는지 합니다. 이렇게 하면 트랜잭션의 안정성이 보장됩니다.
* SSL 오프 로드 – 클라이언트 연결이 설정 된 경우 hello 부하 분산 장치 hello 클라이언트와 hello 부하 분산 장치 간의 세션 hello HTTPS를 사용 하 여 암호화 됩니다 (SSL /) 프로토콜입니다. 하지만, 순서 tooincrease 성능 부하 분산 장치 hello와 hello 부하 분산 사용 하 여 hello (암호화 되지 않은) HTTP 프로토콜 뒤에 웹 서버 hello로 hello 옵션 toohave hello 연결을 해야합니다. 이므로 참조 tooas "SSL 오프 로드" hello 부하 분산 장치 뒤에 웹 서버의 hello 암호화와 관련 된 hello 프로세서 오버 헤드가 발생 하지 않습니다 따라서 수 tooservice 요청을 보다 신속 하 게 이어야 합니다.
* URL 기반 콘텐츠 라우팅-이 기능을 사용 하면 여기서 tooforward 연결 기반 hello 대상 URL에 hello 부하 분산 장치 toomake 결정 합니다. IP 주소에 기반하여 부하 분산 결정을 내리는 솔루션보다 훨씬 더 많은 유연성을 제공합니다.

자세한 정보:

* [응용 프로그램 게이트웨이 개요](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>네트워크 수준 부하 분산
반대로 tooHTTP 기반 부하 분산, 네트워크 수준 부하 분산에 IP 주소와 포트 (TCP 또는 UDP) 번호를 기준으로 분산 결정을 로드 합니다.
수준에서 네트워크 부하 분산 Azure hello Azure 부하 분산 장치를 사용 하 여 hello 이점을 얻을 수 있습니다. Azure 부하 분산 장치 hello의 몇 가지 주요 특징은 다음과 같습니다.

* IP 주소와 포트 번호에 기반한 네트워크 수준 부하 분산
* 모든 응용 프로그램 계층 프로토콜에 대한 지원
* 부하를 분산 tooAzure 가상 컴퓨터 및 클라우드 서비스 역할 인스턴스
* 인터넷 연결(외부 부하 분산) 및 비-인터넷 연결(내부 부하 분산) 응용 프로그램과 가상 컴퓨터 모두에 사용할 수 있음
* 끝점 모니터링을 hello 부하 분산 장치 뒤 hello 서비스 사용 하지 못하게 될 경우 사용 되는 toodetermine 함

자세한 정보:

* [여러 가상 컴퓨터 또는 서비스 간의 인터넷 연결 부하 분산 장치](../load-balancer/load-balancer-internet-overview.md)
* [내부 부하 분산 장치 개요](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>전역 부하 분산
일부 조직에서는 hello 최고 수준의 가용성 가능한 할 됩니다. 이 목표에서 toohost 응용 프로그램을 전체적으로 한 가지 방법은 tooreach 데이터 센터를 분산 합니다. 응용 프로그램 hello 전세계 위치한 데이터 센터에서 호스팅되는 지리적 영역 전체 toobecome 사용 불가 및 여전히가지고 있어야 hello 응용 프로그램에 대 한 가능한 한는 합니다.

또한 호스팅 전 세계적으로 분산된 데이터 센터에서 응용 프로그램으로 가져올 toohello 가용성 장점을 얻을 수 있습니다 성능 혜택. 가장 가까이 hello 요청을 수행 하는 toohello 장치에 있는 hello 서비스 toohello 데이터 센터에 대 한 요청에 지시 하는 메커니즘을 사용 하 여 이러한 성능 이점은 얻을 수 있습니다.

전역 부하 분산은 이러한 두 가지 이점을 모두 제공할 수 있습니다. Azure에서 전역 부하 Azure 트래픽 관리자를 사용 하 여 분산의 hello 이점을 얻을 수 있습니다.

자세한 정보:

* [트래픽 관리자란?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>이름 확인
이름 확인은 Azure에서 호스팅하는 모든 서비스에 대해 중요한 기능입니다. 보안 측면에서 이름 확인 함수 hello 손상 사이트 tooan 공격자의 사이트에서 tooan 공격자가 리디렉션 요청을 발생할 수 있습니다. 보안 이름 확인은 사용자의 모든 클라우드 호스팅 서비스의 요구 사항입니다.

두 가지 유형의 tooaddress 해야 하는 이름 확인에는

* 내부 이름 확인 - 내부 이름 확인은 Azure 가상 네트워크, 온-프레미스 네트워크 또는 둘 다에 있는 서비스에서 사용합니다. 내부 이름 확인에 사용 되는 이름과 hello 인터넷을 통해 액세스할 수 없는 합니다. 이 보안을 최적화에 대 한 내부 이름 확인 체계 tooexternal 액세스할 수 있는 사용자가 아닌지 중요 합니다.
* 외부 이름 확인 - 외부 이름 확인은 온-프레미스와 Azure 가상 네트워크 외부의 사용자 및 장치에서 사용합니다. 이것은 hello 이름이 표시 toohello 인터넷 사용 되는 toodirect 연결 tooyour 클라우드 기반 서비스입니다.

내부 이름 확인에는 두 가지 옵션이 있습니다.

* Azure 가상 네트워크 DNS 서버 - 새 Azure 가상 네트워크를 만들 경우 사용자에 대한 DNS 서버가 만들어집니다. 이 DNS 서버는 Azure 가상 네트워크에 있는 hello 컴퓨터 hello 이름을 확인할 수 있습니다. 이 DNS 서버를 구성할 수 이며 함으로써 보안 이름 확인 솔루션 hello Azure 패브릭 관리자에 의해 관리 됩니다.
* 자체 DNS 서버 가져오기 – 직접 선택한 Azure 가상 네트워크에서 DNS 서버 배치의 hello 옵션이 있습니다. 이 DNS 서버는 Active Directory 통합 DNS 서버 또는 hello Azure Marketplace에서에서 가져올 수 있는 Azure 파트너에서 제공 하는 전용된 DNS 서버 솔루션 수 있습니다.

자세한 정보:

* [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)
* [VNet(가상 네트워크)에서 사용하는 DNS 서버 관리](../virtual-network/virtual-network-manage-network.md#dns-servers)

외부 DNS 확인에는 두 가지 옵션이 있습니다.

* 자체 외부 DNS 서버 온-프레미스 호스팅
* 서비스 공급자를 통해 자체 외부 DNS 서버 호스팅

많은 대규모 조직에서는 자체 DNS 서버 온-프레미스를 호스팅합니다. 전문 기술 및 전역 상태 toodo 하므로 네트워킹 hello 했기 때문에이 수행할 수 있습니다.

대부분의 경우 것이 더 나은 toohost 서비스 공급자를 사용 하 여 DNS 이름 확인 서비스입니다. 이러한 서비스 공급자 네트워크 전문 지식을 hello 및 이름 확인 서비스에 대 한 전역 상태 tooensure 매우 높은 가용성은 합니다. DNS 이름 확인 서비스 장애를 경우 아무도 않기 때문에 서비스에 대 한 가용성 반드시 수 tooreach 인터넷 연결 서비스 여야 합니다.

Azure는 항상 사용 가능한 및 Azure DNS의 hello 형태로 고성능 외부 DNS 솔루션입니다. 이 외부 이름 확인 솔루션에서는 hello 전세계 Azure DNS 인프라를 활용 합니다. Toohost 허용 사용 하 여 Azure에서 도메인을 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 청구 hello 합니다. Azure의 일환으로, hello 플랫폼에 기본 제공 되는 hello 강력한 보안 제어도 상속 합니다.

자세한 정보:

* [Azure DNS 개요](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>DMZ 아키텍처
많은 엔터프라이즈 조직 Dmz toosegment hello 인터넷 및 서비스 간의 해당 네트워크 toocreate 버퍼 놓기 영역을 사용합니다. hello 네트워크의 hello DMZ 부분에는 낮은 수준의 보안 영역으로 간주 됩니다 하 고 우선 순위가 높은 자산이 없습니다 해당 네트워크 세그먼트에 배치 됩니다. 일반적으로 DMZ hello 세그먼트 및 다른 네트워크 인터페이스 연결 된 tooa 네트워크에 있고 가상 컴퓨터 및 hello 인터넷에서에서 인바운드 연결을 허용 하는 서비스에는 네트워크 인터페이스가 있는 네트워크 보안 장치를 볼 수 있습니다.

DMZ 디자인 및 hello 의사 결정 toodeploy DMZ를 차례로 네트워크 보안 요구 사항에 기반 하나, toouse 결정 한 경우 어떤 유형의 DMZ toouse 변화는 여러 가지가 있습니다.

자세한 정보:

* [Microsoft 클라우드 서비스 및 네트워크 보안](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>감사 및 위협 검색

Azure 제공 기능 toohelp이 키에 초기 검색, 모니터링 및 hello 기능 toocollect 및 검토 네트워크 트래픽이 있습니다.

### <a name="azure-network-watcher"></a>Azure Network Watcher
Azure 네트워크 감시자 많은 수의 문제 해결에 도움이 수 있을 뿐만 아니라 보안 문제 hello 식별 도구 tooassist의 완전히 새로운 집합을 제공 하는 기능을 포함 합니다.

[보안 그룹 보기 ](/network-watcher/network-watcher-security-group-view-overview.md) 비교 각 Vm에 대 한 조직 tooeffective 규칙에 의해 정의 된 hello 기준 정책을 프로그래밍 방식으로 감사 사용된 tooperform 수 있으며 가상 컴퓨터의 감사 및 보안 준수 하는 데 도움이 됩니다. 그러면 모든 구성 드리프트를 식별하는 데 도움이 됩니다.

[패킷 캡처](/network-watcher/network-watcher-packet-capture-overview.md) hello 가상 컴퓨터에서 네트워크 트래픽을 tooand toocapture 있습니다. 응용 프로그램의 문제 해결 hello 및 toocollect 네트워크 통계를 허용 하 여 수 있도록 지 원하는 것 외에도 문제 패킷 캡처 네트워크 침입 hello 조사에 유용할 수 있습니다. Azure 기능에 대 한 응답 toospecific Azure toostart 네트워크 캡처와 함께이 기능을 사용할 수도 있습니다 경고 합니다.

Azure 네트워크 감시자와 어떻게 toostart 환경에서 테스트 하는 hello 기능 중 일부에 대해 살펴봅니다 hello에 대 한 자세한 내용은 [Azure 네트워크 감시자 모니터링 개요](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Azure 네트워크 감시자 아직입니다 공개 미리 보기 hello 있을 수 있으므로 동일한 수준의 가용성과 서비스 가용성 릴리스를 일반적으로 안정성. 특정 기능은 지원되지 않을 수 있고, 기능이 제한될 수 있으며 일부 Azure 위치에서 사용하지 못할 수도 있습니다. 에 대 한 hello 최신 알림을 가능 여부와이 서비스의 상태를 확인 hello [Azure 업데이트 페이지](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure 보안 센터
보안 센터를 사용 하면 방지 하 고 검색 toothreats, 응답 하 고에 대 한 가시성 및에 대 한 제어, Azure 리소스의 보안을 hello 증가 제공 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 다양한 보안 솔루션 집합에서 작동합니다.

Azure 보안 센터는 다음과 같은 방법을 통해 네트워크 보안을 최적화하고 모니터링하는 데 도움을 줍니다.

* 네트워크 보안 권장 사항 제공
* 네트워크 보안 구성의 hello 상태 모니터링
* 기반 toonetwork 위협 모두 hello 끝점 및 네트워크 수준에서 경고 표시

자세한 정보:

* [소개 tooAzure 보안 센터](../security-center/security-center-intro.md)


### <a name="logging"></a>로깅
네트워크 수준에서 로깅은 네트워크 보안 시나리오의 핵심 기능입니다. Azure에서 얻은 정보를 네트워크 보안 그룹 tooget 네트워크 수준에 대 한 정보를 기록할 수 있습니다. NSG 로깅을 사용하여 다음에서 정보를 얻습니다.

* [활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) -이러한 로그는 tooview 사용 되는 모든 작업 제출 tooyour Azure 구독. 이러한 로그는 기본적으로 사용 및 hello Azure 포털 내에서 사용할 수 있습니다. 이전에는 이러한 로그를 "감사 로그" 또는 "작업 로그"라고도 했습니다.
* 이벤트 로그 – 어떤 NSG 규칙이 적용 되었는지에 대한 정보를 제공합니다.
* 카운터 로그-이 로그 각 NSG 규칙에 적용 된 toodeny 된 횟수를 알 수 있도록 하거나 트래픽을 허용 합니다.

사용할 수도 있습니다 [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), 강력한 데이터 시각화 도구를 tooview 및 이러한 로그를 분석 합니다.

자세한 정보:

* [NSG(네트워크 보안 그룹)에 대한 Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md)

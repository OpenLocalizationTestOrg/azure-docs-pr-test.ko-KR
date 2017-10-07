---
title: "네트워크 보안에 대 한 유용한 정보 aaaAzure | Microsoft Docs"
description: "이 문서에서는 기본 제공 Azure 기능을 사용한 네트워크 보안 모범 사례를 제공합니다."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Azure 네트워크 보안 모범 사례
Microsoft Azure Azure 가상 네트워크에 배치 하 여 tooconnect 기기 및 가상 컴퓨터 네트워크에 연결 하는 tooother 장치가 활성화 됩니다. Azure 가상 네트워크는 tooconnect 가상 네트워크 인터페이스 카드 tooa 가상 tooallow TCP 기반 간 네트워크 통신 사용 하도록 설정 하는 네트워크 장치를 허용 하는 가상 네트워크 구문입니다. 연결 된 tooan Azure 가상 네트워크에 수 tooconnect toodevices 있는 azure 가상 컴퓨터 동일한 Azure 가상 네트워크에서 인터넷 hello에 서로 다른 Azure 가상 네트워크, hello 또는 사용자 고유의 온-프레미스 네트워크에도 합니다.

이 문서에서는 Azure 네트워크 보안 모범 사례 컬렉션에 대해 설명합니다. 이들 모범 사례는 Azure 네트워킹에 대 한 경험 및 고객의 hello 경험을와 같은 직접 합니다.

각 모범 사례에 대해 다음 사항을 설명하겠습니다.

* 어떤 hello 것이 좋습니다.
* 이유는 tooenable 최선의 방법을
* Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
* 가능한 대안 toohello 모범 사례
* Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

이 Azure 네트워크 보안에 대 한 유용한 정보 문서는 합의 의견 및 Azure 플랫폼 기능 및 기능 집합에 기초이 문서가 작성 된 hello 시 존재 합니다. 의견 및 기술 시간이 지남에 따라 변경 하 고이 문서 됩니다. 이러한 변경 내용을 정기적으로 tooreflect에서 업데이트 합니다.

이 문서에서 다루는 Azure 네트워크 보안 모범 사례에는 다음이 포함됩니다.

* 서브넷을 논리적으로 분할
* 라우팅 동작 제어
* 강제 터널링 적용
* 가상 네트워크 어플라이언스 사용
* DMZ를 배포하여 보안 영역 지정
* 노출 toohello를 인터넷 전용된 WAN 연결을 사용 하지 마십시오.
* 가동 시간 및 성능 최적화
* 전역 부하 분산 사용
* RDP 액세스 tooAzure 가상 컴퓨터를 사용 하지 않도록 설정
* Azure 보안 센터 활성화
* 데이터 센터를 Azure로 확장

## <a name="logically-segment-subnets"></a>서브넷을 논리적으로 분할
[Azure 가상 네트워크](https://azure.microsoft.com/documentation/services/virtual-network/) 온-프레미스 네트워크에 비슷한 tooa LAN 됩니다. hello Azure 가상 네트워크의 기본 개념은 단일 개인 IP 주소 공간 기반 네트워크에 배치할 수 있습니다 모든 만드는 프로그램 [Azure 가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines/)합니다. hello 개인 IP 주소 공간 사용 가능한는 hello 클래스 A (10.0.0.0/8), 클래스 B (172.16.0.0/12) 및 클래스 C에에서 (192.168.0.0/16) 범위.

비슷한 toowhat 있습니다 않는 온-프레미스, 서브넷으로 toosegment hello 큰 주소 공간을 해도 됩니다. 사용할 수 있습니다 [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) 원칙 toocreate 서브넷 서브넷 지정을 기반으로 합니다.

자동으로 수행 됩니다 서브넷 간의 라우팅 및 않아도 toomanually 라우팅 테이블을 구성 합니다. 그러나 hello 기본 설정은 hello Azure 가상 네트워크에 만들 hello 서브넷 사이 네트워크 액세스 컨트롤이 없는입니다. 순서 toocreate 네트워크 액세스 제어 서브넷 간의 해야 tooput hello 서브넷 사이입니다.

이 작업은 tooaccomplish를 사용할 수 hello 작업 중 하나는 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) (NSG). Nsg는 간단한 상태 저장 패킷 검사 네트워크 트래픽에 대 한 허용/거부 규칙 toocreate hello 5-튜플 (hello 원본 IP, 원본 포트, 대상 IP, 대상 포트 및 프로토콜 계층 4)를 사용 하는 장치에 접근 합니다. 허용 하거나 단일 IP 주소, 여러 개의 IP 주소에서 tooand 또는 짝수 tooand 전체 서브넷에서의 트래픽을 tooand 거부할 수 있습니다.

네트워크 액세스 제어 서브넷 간의 있습니다 toohello 속하는 tooput 리소스 Nsg를 사용 하 여 동일한 보안 영역 또는 자신의 서브넷에 있는 역할입니다. 웹 계층, 응용 프로그램 논리 계층, 데이터베이스 계층으로 구성된 간단한 3계층 응용 프로그램을 예로 들 수 있습니다. 이러한 계층의 tooeach 고유 서브넷에 속한 가상 컴퓨터를 배치할 수 있습니다. Hello 서브넷 간의 Nsg toocontrol 트래픽을 사용할 수 있습니다.

* 웹 계층 가상 컴퓨터 연결 toohello 응용 프로그램 논리 컴퓨터를 시작할만 수 있으며는 hello 인터넷에서 연결
* 응용 프로그램 논리 가상 컴퓨터와 데이터베이스 계층의 연결을 시작할만 수 있으며는 hello 웹 계층의 연결
* 데이터베이스 계층 가상 컴퓨터 자체의 서브넷 외부에서 어디에도 연결을 시작할 수 없습니다 및 hello 응용 프로그램 논리 계층에서 연결을 허용할만 수 있습니다.

네트워크 보안 그룹 및 사용 하는 방법으로 toologically 세그먼트에 대 한 자세한 toolearn Azure 가상 네트워크 문서를 참조 하세요 hello [네트워크 보안 그룹 이란](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>라우팅 동작 제어
Azure 가상 네트워크에서 가상 컴퓨터를 배치할 때 해당 hello 가상 컴퓨터 tooany 다른 가상 컴퓨터를 연결할 수 있습니다 알 수 있습니다 hello 다른 가상 컴퓨터는 서로 다른 서브넷에 있는 경우에 hello 동일한 Azure 가상 네트워크에 있습니다. 왜 이것이 가능 hello 이유 기본적으로 설정 되어 이러한 유형의 통신을 허용 하는 시스템 경로 컬렉션을 된다는 점입니다. 이러한 기본 경로 hello에 가상 컴퓨터 (아웃 바운드 통신 toohello 인터넷만)에 대 한 인터넷 hello로 하 고, 동일한 Azure 가상 네트워크 tooinitiate 연결을 허용 합니다.

Hello 기본 시스템 경로 다양 한 배포 시나리오에 유용 하지만, 하려는 toocustomize hello 라우팅 구성, 배포 하는 경우가 있습니다. 이러한 사용자 지정 하면 tooconfigure hello 다음 홉 주소 tooreach 특정 대상 있습니다.

가상 네트워크 보안 어플라이언스를 배포할 때에는 사용자 정의 경로를 구성하는 것이 좋습니다. 이에 대해서는 뒷부분에 나오는 모범 사례에서 설명하겠습니다.

> [!NOTE]
> 사용자 정의 경로 필요 하지 않으며 hello 기본 시스템 경로입니다. 대부분의 경우에서 작동 합니다.
>
>

사용자 정의 경로 대 한 자세히 알아볼 수 있습니다 및 방법을 tooconfigure hello 문서를 참조 하 여 이러한 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)합니다.

## <a name="enable-forced-tunneling"></a>강제 터널링 적용
강제 터널링 toobetter 이해에 어떤 "분할 터널링"은 유용한 toounderstand 합니다.
분할 터널링의 hello 가장 일반적인 예는 VPN 연결으로 표시 됩니다. 호텔 대화방 tooyour 회사 네트워크에서 VPN 연결을 설정 한다고 가정 합니다. 이 연결 tooconnect tooresources 회사 네트워크에 있으며 hello VPN 터널을 통해 회사 네트워크의 모든 통신 tooresources 이동 합니다.

Hello 인터넷에서 tooconnect tooresources 하려는 경우 어떻게 되나요? 분할 터널링을 사용 하면 이러한 연결은 직접 toohello 인터넷 이동한 다음 hello VPN 통해서가 아니라 터널링 합니다. 일부 보안 전문가이 toobe 잠재적인 위험을 고려 하 고 따라서 분할 터널링 사용할 수 없도록 것이 좋습니다. 및 모든 연결 hello 인터넷의 대상이 되 고 회사 리소스에 대해 대상이 지정 되었으며 다른 hello VPN 터널을 통해 이동 합니다. 이 작업의 hello 이점은 인터넷 hello VPN 클라이언트 hello VPN 터널 외부 toohello 인터넷 연결 경우 hello 사례 수 없게 hello 회사 네트워크 보안 장치를 통해 강제 적용 한 다음 해당 연결 toohello 점입니다.

이제이 상태로 전환 해 보겠습니다 Azure 가상 네트워크에 toovirtual 컴퓨터를 백업 합니다. Azure 가상 네트워크에 대 한 hello 기본 경로 가상 컴퓨터 tooinitiate 트래픽 toohello 인터넷을 허용합니다. 이 너무으로 나타낼 수 있습니다 보안상 위험을 아웃 바운드 연결에 이러한 가상 컴퓨터의 hello 공격 노출 영역은 그만큼 늘어납니다 수 및 공격자가 기능을 활용할 수 있습니다.
이러한 이유로 Azure 가상 네트워크와 온-프레미스 네트워크 간에 크로스-프레미스 연결이 있는 경우 가상 컴퓨터에서 강제 터널링을 활성화하는 것이 좋습니다. 크로스 프레미스 연결에 대한 내용은 이 Azure 네트워킹 모범 사례 문서의 뒷부분에서 다루겠습니다.

네트워크 보안 그룹 (앞에서 설명한) 또는 Azure의 이용 있는지 확인 크로스 프레미스 연결이 없는 경우 가상 네트워크 보안 어플라이언스 (다음 단원에서 설명된) tooprevent 아웃 바운드 연결 toohello 인터넷에서 Azure 가상 컴퓨터입니다.

에 대해 더 알아봅니다 toolearn 강제 터널링 어떻게 tooenable, 문서를 참조 하세요 hello 및 [구성 강제 터널링 PowerShell 및 Azure 리소스 관리자를 사용 하 여](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md)합니다.

## <a name="use-virtual-network-appliances"></a>가상 네트워크 어플라이언스 사용
네트워크 보안 그룹 및 사용자 정의 된 라우팅을 제공할 수는 어느 정도의 hello에서 네트워크 보안 네트워크 및 전송 계층의 hello 동안 [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 하려고 하거나 tooenable 필요 합니다 toobe 상황 것 이며 hello 스택의 높은 수준에서 보안입니다. 이러한 상황에서는 Azure 파트너가 제공하는 가상 네트워크 보안 어플라이언스를 배포하는 것이 좋습니다.

Azure 네트워크 보안 어플라이언스는 네트워크 수준 제어에서 제공하는 보안 수준을 대폭 강화할 수 있습니다. 가상 네트워크 보안 어플라이언스에서 제공 하는 hello 네트워크 보안 기능 중 일부는 다음과 같습니다.

* 방화벽
* 침입 감지/침입 방지
* 취약점 관리
* 응용 프로그램 제어
* 네트워크 기반 이상 감지
* 웹 필터링
* 바이러스 백신
* 봇 넷 보호

네트워크 수준 액세스 제어를 통해 얻을 수 있는 것보다 높은 수준의 네트워크 보안이 필요한 경우 Azure 가상 네트워크 보안 어플라이언스를 살펴보고 배포할 것을 권장합니다.

어떤 Azure 가상 네트워크 보안 어플라이언스를 사용할 수 있는 기능에 대 한 toolearn hello를 방문 하십시오 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) "보안" 및 "네트워크 보안"으로 검색 합니다.

## <a name="deploy-dmzs-for-security-zoning"></a>DMZ를 배포하여 보안 영역 지정
DMZ "경계 네트워크" 실제 있거나에 해당 하는 논리 네트워크 세그먼트 tooprovide 자산과 hello 인터넷 사이 보안에 대 한 추가 수준의 설계 되었습니다. hello DMZ의 hello 목적은 tooplace hello 네트워크 보안 장치 과거와 Azure 가상 네트워크에 원하는 트래픽만 허용 되도록 hello hello DMZ 네트워크 가장자리에서 네트워크 액세스 제어 장치 특수화입니다.

Dmz 유용 되므로 모니터링, 로깅 및 Azure 가상 네트워크의 hello 가장자리에 hello 장치에 대 한 보고에 네트워크 액세스 제어 관리에 집중할 수 있습니다. 여기서 일반적으로 DDoS 방지, 침입 감지/침입 방지 시스템(IDS/IPS), 방화벽 규칙 및 정책, 웹 필터링, 네트워크 맬웨어 방지 프로그램 등을 활성화합니다. hello 네트워크 보안 장치 hello 인터넷 및 Azure 가상 네트워크 사이 및 두 네트워크 인터페이스가 있어야 합니다.

DMZ의 기본 디자인 hello 이지만는 다른 많은 DMZ 디자인와 같은 연속, 트라이 홈, 다중 홈 등과 합니다.

에 대해 권장 모든 고급 보안의 배포는 DMZ tooenhance hello 수준의 Azure 리소스에 대 한 네트워크 보안을 배포 하도록 고려 합니다.

Dmz와 어떻게 toodeploy Azure에서 해당 문서를 참조 하세요 hello에 대 한 자세한 toolearn [Microsoft 클라우드 서비스 및 네트워크 보안](../best-practices-network-security.md)합니다.

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>노출 toohello를 인터넷 전용된 WAN 연결을 사용 하지 마십시오.
대부분의 조직에서는 hello 하이브리드 IT 경로 선택 했습니다. 하이브리드 IT 환경에서 hello 회사의 정보 자산 중 일부는 azure에서 다른 온-프레미스로 유지 합니다. 서비스의 구성 요소 중 일부는 Azure에서 실행되고 나머지 구성 요소는 온-프레미스에서 실행되는 경우가 많습니다.

Hello 하이브리드 IT 시나리오에서에서 크로스-프레미스 연결의 일부 종류 일반적으로 합니다. 이 크로스-프레미스 연결 hello 회사 tooconnect 자신의 온-프레미스 네트워크 tooAzure 가상 네트워크를 허용 합니다. 다음과 같은 두 가지 크로스-프레미스 연결 솔루션이 제공됩니다.

* 사이트 간 VPN
* ExpressRoute

[사이트 간 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)은 온-프레미스 네트워크와 Azure 가상 네트워크 간의 가상 사설 연결을 나타냅니다. 이 연결이 이루어집니다 인터넷 hello를 사용 하면 너무 "터널"은 암호화 된 연결 하면 네트워크와 Azure 내에서 정보 계속 합니다. 사이트 간 VPN은 수십 년 동안 모든 규모의 기업에서 배포해 온 안전하고 완성도 높은 기술입니다. 터널 암호화는 [IPsec 터널 모드](https://technet.microsoft.com/library/cc786385.aspx)를 사용하여 수행됩니다.

사이트 간 VPN은 안정적이 고 설정 된 신뢰할 수 있는 기술, hello 터널 내의 트래픽을 인터넷 hello를 트래버스하여 합니다. 또한 대역폭은 상대적으로 제한 된 tooa 200Mbps에 대 한 최대입니다.

크로스-프레미스 연결에 강력한 보안 또는 성능 수준이 필요한 경우 크로스-프레미스 연결에 Azure ExpressRoute를 사용하는 것이 좋습니다. ExpressRoute는 온-프레미스 위치 또는 Exchange 호스팅 공급자 사이의 WAN 링크입니다. Telco 연결 이므로 데이터 hello 인터넷을 통해 전송 하지 않습니다 이며 노출된 되지 toohello 인터넷 통신에 내재 된 잠재적 위험 합니다.

Azure ExpressRoute 작동 하는 방법에 대 한 자세한 toolearn 어떻게 toodeploy, 문서를 참조 하세요 hello 및 [express 경로 기술 개요](../expressroute/expressroute-introduction.md)합니다.

## <a name="optimize-uptime-and-performance"></a>가동 시간 및 성능 최적화
기밀성, 무결성 및 가용성 CIA ()는 오늘날의 가장 강력한 보안 모델의 hello 두꺼운 수직선을 구성 됩니다. 기밀성은 암호화 및 개인 정보에 대 한, 무결성은 권한 없는 사람이 데이터는 변경 되지 않습니다 및 가용성은 권한 있는 개인 권한이 수 tooaccess hello 정보 해야 하는 방법에 대 한 확인 tooaccess 합니다. 이러한 영역 중 하나에서 오류가 발생하면 잠재적 보안 위반이 있다는 뜻입니다.

가용성은 가동 시간 및 성능에 대한 것으로 생각할 수 있습니다. 서비스가 중지되면 정보에 액세스할 수 없습니다. 성능이 하므로 저하 toomake hello 데이터를 사용할 수 없는 경우 다음 수 이라고 생각 hello 데이터 toobe 액세스할 수 없습니다. 따라서 어떤 toodo 필요 보안 측면에서 서비스의 최적의 작동 시간 및 성능 있는지 toomake 수 있습니다.
널리 사용 되 고 효과적인 방법 tooenhance 가용성 사용 되며 성능 toouse 부하를 분산 합니다. 부하 분산은 서비스에 포함된 서버 간에 네트워크 트래픽을 분산하는 방법입니다. 예를 들어 서비스의 일부로 프런트 엔드 웹 서버를 설정한 경우에 여러 프런트 엔드 웹 서버 간에 분산 toodistribute hello 트래픽 부하를 사용할 수 있습니다.

이 배포 트래픽의 hello 부하 분산 장치는 트래픽 toothat 서버 및 온라인 상태인 리디렉션 트래픽 toohello 서버 전송을 중지 hello 웹 서버 중 하나를 사용할 수 없는 경우 때문에 가용성이 증가 됩니다. 부하 분산 hello 프로세서, 네트워크 및 메모리 오버 헤드의 요청 처리를 분산 되어 모든 hello 부하 분산 된 서버 때문에 성능에도 도움이 됩니다.

서비스에 적합하다면 되도록이면 부하 분산을 사용하는 것이 좋습니다. 적합성 hello 다음 섹션에서에서 설명 합니다.
Azure 가상 네트워크 수준 hello, Azure는 세 가지 기본 부하 분산 옵션 제공:

* HTTP 기반 부하 분산
* 외부 부하 분산
* 내부 부하 분산

## <a name="http-based-load-balancing"></a>HTTP 기반 부하 분산
HTTP 기반 부하 분산 hello HTTP 프로토콜의 특성을 사용 하 여 어떤 서버 toosend 연결에 대 한 결정으로 계산 됩니다. Azure 응용 프로그램 게이트웨이의 hello 이름으로 이동 하는 HTTP 부하 분산 장치를 있습니다.

다음과 같은 경우에는 Azure 응용 프로그램 게이트웨이를 사용하는 것이 좋습니다.

* 응용 프로그램 요청 해야 하는 hello에서 동일한 사용자/클라이언트 세션 tooreach hello 동일한 백 엔드 가상 컴퓨터. 이 작업의 예는 쇼핑 카트 앱 및 웹 메일 서버가 될 것입니다.
* 응용 프로그램 게이트웨이 활용 하 여 오버 헤드는 toofree 웹 서버 팜에서 SSL 종료에서 응용 프로그램을 [SSL 오프 로드](https://f5.com/glossary/ssl-offloading) 기능입니다.
* Hello 같은 장기 실행 TCP 연결 toobe 라우팅되거나 로드 균형 잡힌된 toodifferent 백 엔드 서버에서 여러 HTTP 요청을 필요로 하는 콘텐츠 배달 네트워크 등의 응용 프로그램.

Azure 응용 프로그램 게이트웨이 작동 방식 및 배포에서 하기를 사용 하는 방법을 자세히 toolearn hello 문서를 참조 하세요 [응용 프로그램 게이트웨이 개요](../application-gateway/application-gateway-introduction.md)합니다.

## <a name="external-load-balancing"></a>외부 부하 분산
외부 부하 분산 hello 인터넷에서에서 들어오는 연결 부하를 Azure 가상 네트워크에 있는 서버 사이 분산 하는 경우 수행이 됩니다. hello Azure 외부 부하 분산 장치이 기능을 제공할 수 있습니다이 고 hello 고정 세션을 필요한 일정 하지 않거나 SSL 오프 로드 하는 경우 사용 하는 것이 좋습니다.

반대로 tooHTTP 기반 부하 분산, 외부 부하 분산 장치 hello hello OSI 네트워킹 모델 toomake 결정 사항에 어떤 서버 tooload 균형 연결에서의 hello 네트워크와 전송 계층에서 정보를 사용합니다.

사용 하는 외부 부하 분산 있을 때마다 권장 [상태 비저장 응용 프로그램](http://whatis.techtarget.com/definition/stateless-app) hello 인터넷에서에서 들어오는 요청을 수락 합니다.

hello Azure 외부 부하 분산 장치의 작동 방식 및 배포 하는 방법,에 대해 자세히 toolearn hello 문서를 참조 하세요 [PowerShell을 사용 하는 리소스 관리자에는 인터넷 연결 부하 분산 장치를 만들기 전에](../load-balancer/load-balancer-get-started-internet-arm-ps.md)합니다.

## <a name="internal-load-balancing"></a>내부 부하 분산
비슷한 tooexternal는 내부 부하 분산 부하 분산 및 사용 하 여 hello 동일한 메커니즘 tooload 균형 연결 toohello 서버 뒤에 있습니다. hello만 차이점은 hello 부하 분산 장치는이 경우에 연결을 수락 hello 인터넷에 없는 가상 컴퓨터에서입니다. 대부분의 경우에서 hello 연결 부하 분산을 위해 허용 되는 Azure 가상 네트워크의 장치에 의해 시작 됩니다.

Tooload 균형 연결 tooSQL 서버 또는 내부 웹 서버의 필요한 경우 등이 기능을 활용 하는 시나리오의 내부 부하 분산을 사용 하는 것이 좋습니다.

Azure 내부 부하 분산의 작동 방식 및 배포 하는 방법,에 대해 자세히 toolearn hello 문서를 참조 하세요 [PowerShell을 사용 하는 내부 부하 분산 장치를 만들기 전에](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer)합니다.

## <a name="use-global-load-balancing"></a>전역 부하 분산 사용
공용 클라우드 컴퓨팅 가능 하 게 toodeploy 전체적으로 배포 된 hello world 전 세계 데이터 센터에 있는 구성 요소를 가진 응용 프로그램입니다. Microsoft Azure에서 가능한 tooAzure의 글로벌 데이터 센터의 현재 상태 때문입니다. 반대로 toohello 로드 균형 조정 기술 앞에서 언급 한, 전역 부하 분산 가능한 toomake 서비스 사용할 수 있도록 전체 데이터 센터 수 없게 되는 경우에 합니다.

[Azure 트래픽 관리자](https://azure.microsoft.com/documentation/services/traffic-manager/)를 활용하여 Azure에서 이 유형의 전역 부하 분산을 사용할 수 있습니다. 트래픽 관리자는 분석이 가능한 tooload 균형 조정 모드 hello 사용자의 hello 위치를 기반으로 연결 tooyour 서비스입니다.

예를 들어 hello 사용자 hello EU에서에서 요청 tooyour 서비스를 하는 hello 연결이 tooyour 방향이 지정 된 서비스는 EU 데이터 센터에 있는 것입니다. 이 부분에서는 트래픽 관리자 전역 부하 균형 잡힌 통해 tooimprove 성능 데이터 센터에 가장 가까운 toohello 연결 하므로 더 멀리 떨어져 있는 toodatacenters 연결 보다 빠릅니다.

Hello 가용성 측면에서 전역 부하 분산 사용 하면 서비스를 사용할 수 있는 전체 데이터 센터는 사용할 수 없게 해야 하는 경우에 합니다.

예를 들어, Azure 데이터 센터 해야 tooenvironmental 이유 나 기한 인해 사용할 수 없는 경우 toooutages tooyour 서비스 것 연결 (예: 지역 네트워크 오류), 온라인 데이터 센터에 가장 가까운 toohello 다시 라우팅합니다. 이 전역 부하 분산은 트래픽 관리자에서 만들 수 있는 DNS 정책을 활용하여 수행됩니다.

광범위 한 분산 범위가 여러 영역으로 이루어지며 hello 최고 수준의 가동 시간을 가능한 클라우드 솔루션 개발에 대 한 트래픽 관리자를 사용 하는 것이 좋습니다.

Azure 트래픽 관리자에 대 한 자세한 toolearn 어떻게 toodeploy, 문서를 참조 하세요 hello 및 [란 트래픽 관리자](../traffic-manager/traffic-manager-overview.md)합니다.

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>RDP/SSH 액세스 tooAzure 가상 컴퓨터를 사용 하지 않도록 설정
가능한 tooreach Azure 가상 컴퓨터는 hello를 사용 하 여 [원격 데스크톱 프로토콜](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) 및 hello [보안 셸](https://en.wikipedia.org/wiki/Secure_Shell) (SSH) 프로토콜입니다. 이러한 프로토콜 가능한 toomanage 가상 컴퓨터 원격 위치에서 하 고는 표준 데이터 센터를 계산 합니다.

hello hello 인터넷을 통해 이러한 프로토콜을 사용 하 여 잠재적인 보안 문제는 공격자가 다양 한 사용할 수 있는 [무작위](https://en.wikipedia.org/wiki/Brute-force_attack) 기술 toogain 액세스 tooAzure 가상 컴퓨터. Hello 공격자가 액세스를 얻은 후 Azure 가상 네트워크에 있는 다른 컴퓨터를 손상 시 키 지에 대 한 시작 지점으로 가상 컴퓨터를 사용 하거나 Azure 외부에서 네트워크 장치 공격 수 있습니다.

이 때문에 직접 RDP 및 SSH 액세스 tooyour Azure 가상 컴퓨터에서 인터넷 hello 사용 하지 않도록 설정 하는 것이 좋습니다. 직접 RDP 및 SSH로 인터넷을 사용할 수 없습니다. hello에서 액세스는 다른 옵션을 원격 관리에 대 한 tooaccess 이러한 가상 컴퓨터를 사용할 수 있습니다.

* 지점 및 사이트 간 VPN
* 사이트 간 VPN
* ExpressRoute

[지점 및 사이트 간 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)은 원격 액세스 VPN 클라이언트/서버 연결의 또 다른 용어입니다. 지점-사이트 VPN hello 인터넷을 통해 단일 사용자 tooconnect tooan을 Azure 가상 네트워크를 수 있습니다. Hello 지점 및 사이트 간 연결이 설정 되, hello 수 수 toouse RDP 또는 SSH tooconnect tooany hello Azure 가상 네트워크에 있는 사용자를 hello 하는 연결 된 가상 컴퓨터 toovia 지점-사이트 후 VPN. 이 가정 해당 hello 사용자가 권한 있는 tooreach 해당 가상 컴퓨터.

지점-사이트 VPN hello 사용자에 게 tooa 가상 컴퓨터를 연결 하기 전에 두 번 tooauthenticate 되므로 직접 RDP 또는 SSH 연결 보다 더 안전 합니다. 첫째, 사용자 요구 tooauthenticate hello (및 권한을 부여할) tooestablish hello 지점-사이트 VPN 연결 둘째, 사용자 요구 tooauthenticate hello (및 권한을 부여할) tooestablish hello RDP 또는 SSH 세션입니다.

A [사이트 간 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) hello 인터넷을 통해 전체 네트워크 tooanother 네트워크를 연결 합니다. 온-프레미스 네트워크 tooan Azure 가상 네트워크 사이트 간 VPN tooconnect를 사용할 수 있습니다. 사이트 간 VPN을 배포 하는 경우 온-프레미스 네트워크의 사용자가 Azure 가상 네트워크의 수 tooconnect toovirtual 컴퓨터 hello RDP를 사용 하 여 인지 또는 사이트 간 VPN 연결을 hello를 않아도 직접 RDP 또는 SSH tooallow 계속 SSH 프로토콜 hello 인터넷을 통해 액세스 합니다.

전용된 WAN 링크 tooprovide 비슷한 toohello 기능을 사용할 수도 있습니다 사이트 간 VPN. hello 주요 차이점은 1입니다. 인터넷, hello 및 2 hello 전용된 WAN 링크 순회 하지 않습니다. 2. 전용 WAN 링크가 일반적으로 더 안정적이고 성능이 뛰어납니다. Azure의 hello 형태로 전용된 WAN 링크 솔루션 제공 [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/)합니다.

## <a name="enable-azure-security-center"></a>Azure 보안 센터 활성화
Azure 보안 센터를 사용 하면 방지 하 고 검색 toothreats, 응답 하 고에 대 한 가시성 및에 대 한 제어, Azure 리소스의 보안을 hello 증가 제공 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

Azure 보안 센터는 다음과 같은 방법을 통해 네트워크 보안을 최적화하고 모니터링하는 데 도움을 줍니다.

* 네트워크 보안 권장 사항 제공
* 네트워크 보안 구성의 hello 상태 모니터링
* 기반 toonetwork 위협 모두 hello 끝점 및 네트워크 수준에서 경고 표시

모든 Azure 배포에서 Azure 보안 센터를 활성화하는 것이 좋습니다.

Azure 보안 센터와 어떻게 tooenable 배포를 위한 해당 문서를 참조 하세요 hello에 대 한 자세한 toolearn [소개 tooAzure 보안 센터](../security-center/security-center-intro.md)합니다.

## <a name="securely-extend-your-datacenter-into-azure"></a>데이터 센터를 Azure로 안전하게 확장
많은 엔터프라이즈 IT 조직은 온-프레미스 데이터 센터를 원활 증가 하는 대신 hello 클라우드를 tooexpand를 검토 하 고 있습니다. 이 확장 hello 공용 클라우드로 기존 IT 인프라의 확장을 나타냅니다. 크로스-프레미스 가능한 tootreat는 연결 옵션을 이용 하 여 Azure 가상 네트워크가 온-프레미스에 또 다른 서브넷으로 인프라를 네트워크입니다.

그러나 계획을 많이 않으며 toobe 해야 하는 디자인 문제 해결 첫 번째입니다. 이 네트워크 보안의 hello 영역에 특히 중요 합니다. 하나 hello 가장 좋은 방법으로 toounderstand toosee 예로 이러한 디자인 접근 방법입니다.

Hello 만들었습니다 [데이터 센터 확장 참조 아키텍처 다이어그램](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) 하 고는 이러한 데이터 센터 확장 모양을 이해 부속 toohelp를 지원 합니다. 이 예제 참조 구현은 tooplan를 사용할 수 있으며 안전한 기업 데이터 센터 확장 toohello 클라우드 디자인을 제공 합니다. 이 문서 tooget 보안 솔루션의 주요 구성 요소 hello의 아이디어를 검토 하는 것이 좋습니다.

toosecurely을 Azure로 데이터 센터를 확장 하는 방법에 대 한 자세한 toolearn hello 비디오를 참조 하십시오 [트 데이터 센터 확장 tooMicrosoft Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA)합니다.

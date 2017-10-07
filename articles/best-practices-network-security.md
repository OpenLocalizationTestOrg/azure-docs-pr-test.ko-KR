---
title: "aaaAzure 네트워크 보안 모범 사례 | Microsoft Docs"
description: "보안 네트워크 환경을 만드는 Azure toohelp에서 사용할 수 있는 hello 주요 기능 중 일부에 대해 알아봅니다"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Microsoft Cloud Services 및 네트워크 보안
Microsoft 클라우드 서비스는 대규모 서비스와 인프라, 엔터프라이즈급 기능 및 여러 하이브리드 연결 옵션을 제공합니다. 고객 tooaccess hello 인터넷을 통해 또는 개인 네트워크 연결을 제공 하는 Azure ExpressRoute와 이러한 서비스를 선택할 수 있습니다. hello Microsoft Azure 플랫폼에는 고객을 tooseamlessly hello 클라우드로 인프라를 확장 하 고 다중 계층 아키텍처를 구축할 수 있습니다. 또한 타사 보안 서비스 및 가상 어플라이언스를 통해 향상된 기능을 구현할 수 있습니다. 이 백서에서는 Express 경로를 통해 액세스하는 Microsoft 클라우드 서비스 사용할 때 고객이 고려해야 하는 보안 및 아키텍처 문제에 대해 개괄적으로 설명합니다 또한 Azure Virtual Network에서 더 안전한 서비스를 만드는 과정을 다룹니다.

## <a name="fast-start"></a>빠른 시작
다음 논리 차트 hello hello Azure 플랫폼에서 사용할 수 있는 여러 보안 방법 있습니다 tooa 구체적인 예의 hello 전달할 수 있습니다. 빠른 참조를 hello 예제를 케이스에 가장 맞는 환경을 찾습니다. 확장 된 설명은 hello 용지를 읽는 계속 합니다.
[![0]][0]

[예제 1: 경계 네트워크 (DMZ, 완충 지역 또는 스크린 된 서브넷이 라고도 함) 빌드 toohelp (Nsg) 네트워크 보안 그룹으로 응용 프로그램을 보호 합니다.](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[예제 2: 빌드는 경계 네트워크 toohelp 방화벽 Nsg와 응용 프로그램을 보호 합니다.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[예제 3: 빌드는 경계 네트워크 toohelp 방화벽, 사용자 정의 경로 (UDR) 및 NSG는 네트워크를 보호 합니다.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[예제 4: 사이트 간 가상 어플라이언스 VPN(가상 사설망)에 하이브리드 연결 추가](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[예제 5: 사이트 간 Azure VPN Gateway를 통한 하이브리드 연결 추가](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[예제 6: ExpressRoute를 통한 하이브리드 연결 추가](#example-6-add-a-hybrid-connection-with-expressroute)</br>
가상 네트워크, 높은 가용성 및 서비스 체인 간 연결 추가 대 한 예제 toothis 문서 동안 추가 hello 앞으로 몇 개월입니다.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Microsoft 규정 준수 및 인프라 보호
toohelp 조직 national 지역 따르고 hello 수집 및 개인 데이터의 사용과 관련 된 특정 업계 요구 사항, Microsoft는 40 개 이상의 인증 및 증명 제공 합니다. 모든 클라우드 서비스 공급자의 가장 종합적인 hello 설정합니다.

자세한 내용은 hello에 hello 준수 정보 참조 [Microsoft 보안 센터][TrustCenter]합니다.

Microsoft는 포괄적인 접근 방식 tooprotect 클라우드는 데 필요한 인프라 toorun 대규모 글로벌 서비스에 있습니다. 하드웨어, 소프트웨어, 네트워크, Microsoft 클라우드 인프라에 포함 된 관리 및 또한 toohello 물리적 데이터 센터 운영 담당자 및 합니다.

![2]

이 방법은 toodeploy 고객에 대 한 보다 안전한 기반 Microsoft 클라우드 hello에이 서비스를 제공합니다. 다음 단계 hello 고객 toodesign 되며 보안 아키텍처 tooprotect 이러한 서비스를 만듭니다.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>기존 보안 아키텍처 및 경계 네트워크
하지만 Microsoft 연구 하 고 과도 하 게 보호 하는 hello 클라우드 인프라를 클라우드 서비스 및 리소스 그룹 고객도 보호 해야 합니다. 다중 계층된 접근 방식을 toosecurity hello 최상의 철저 한 방어를 제공합니다. 경계 네트워크 보안 영역은 신뢰할 수 없는 네트워크로부터 내부 네트워크 리소스를 보호합니다. 경계 네트워크 toohello 모서리나 hello 인터넷 및 보호 하는 hello 엔터프라이즈 IT 인프라 사이 hello 네트워크의 부분을 참조 합니다.

일반적인 엔터프라이즈 네트워크에서 hello 핵심 인프라는 여러 계층의 보안 장치 사용 hello 경계에서 대형 과도 하 게 합니다. hello 경계 각 계층의 장치 및 정책 적용 지점으로 구성 됩니다. 각 계층에는 hello 네트워크 보안 장치 뒤의 조합이 포함 될 수 있습니다: 방화벽, 서비스 거부 (DoS) 방지, 침입 감지 또는 보호 시스템 ID/IP (), 및 VPN 장치입니다. 정책 적용 hello 형태의 방화벽 정책, 액세스 제어 목록 (Acl) 또는 특정 라우팅 걸릴 수 있습니다. hello 최전방의 방어선 hello 네트워크에서 직접 hello 인터넷에서에서 들어오는 트래픽을 수락은 hello 네트워크에 합법적인 요청이 추가 허용 하면서 이러한 메커니즘 tooblock 공격 및 유해한 트래픽이의 조합입니다. 이 트래픽을 라우팅합니다 hello 경계 네트워크에 직접 tooresources를 합니다. 해당 리소스 수 다음와 "통신" tooresources 유효성 검사에 대 한 다음 경계 hello를 통해 전송 되는 hello 네트워크에 자세히 첫 번째입니다. hello 가장 바깥쪽 레이어 hello 네트워크의이 부분에 노출 된 toohello 일종의 양쪽 모두에 대 한 보호를 사용 하 여 일반적으로 인터넷 이므로 hello 경계 네트워크를 라고 합니다. hello 다음 그림은 예 단일 서브넷 경계 네트워크의 두 개의 보안 경계와 회사 네트워크에서.

![3]

경계 네트워크는 많은 아키텍처가 사용 tooimplement 합니다. 이러한 아키텍처는 각 경계 tooblock 트래픽에서 다양 한 메커니즘으로 간단한 부하 분산 장치 tooa 다중 서브넷 경계 네트워크에서 다양 하 고 hello 회사 네트워크의 hello 더 깊은 계층을 보호할 수 있습니다. Hello 경계 네트워크 작성 방법은 hello hello 조직과 전반적인 위험 허용 오차의 특정 요구에 따라 달라 집니다.

고객의 이동 된 워크 로드 toopublic 클라우드 때 Azure toomeet 규정 준수 및 보안 요구 사항에 경계 네트워크 아키텍처에 대 한 중요 한 toosupport 기능 합니다. 이 문서는 고객이 Azure에서 보안 네트워크 환경을 빌드하는 방법에 대한 지침을 제공합니다. Hello 경계 네트워크에 중점을 두고 하지만 네트워크 보안의 여러 측면에 대 한 포괄적인 설명은 포함 됩니다. hello 다음 질문이이 설명을 게 알립니다.

* Azure에서 경계 네트워크를 빌드하는 방법
* Hello Azure 기능 사용 가능한 toobuild hello 경계 네트워크의 일부 무엇입니까?
* 백 엔드 워크로드 보호 방법
* Azure에서 인터넷 통신 제어 toohello 작업은 무엇입니까?
* Azure에서 배포에서 hello 온-프레미스 네트워크를 어떻게 보호 수 있습니다.?
* 타사 어플라이언스나 서비스에 기본 Azure 보안 기능을 사용하는 방법

다이어그램을 다음 hello 다양 한 Azure toocustomers에서 제공 하는 보안 계층을 보여 줍니다. 이러한 계층은 모두 hello 자체 Azure 플랫폼에서에서 네이티브과 고객 정의 기능입니다.

![4]

Azure에 대 한 대규모 공격 으로부터 보호 하는 Azure DDoS hello 인터넷에서에서 인바운드 합니다. hello 다음 계층은 고객이 정의한 공용 IP 주소 (끝점)는 사용 되는 toodetermine hello 클라우드 서비스 toohello 가상 네트워크를 통해 트래픽을 전달할 수 있습니다. 기본 Azure Virtual Network 격리를 통해 모든 타 네트워크를 격리하고 트래픽이 사용자가 구성한 경로 및 방법을 통해서만 전달되도록 할 수 있습니다. 이러한 경로 메서드는 Nsg, UDR, 및 네트워크 가상 어플라이언스 hello 보호 네트워크 toocreate 사용 되는 보안 경계 tooprotect hello 응용 프로그램 배포를 될 수 있는 hello 다음 계층.

hello 다음 섹션에서는 Azure 가상 네트워크에 대 한 개요를 제공 합니다. 이러한 Virtual Network는 고객이 만들며 배포된 워크로드가 연결되는 대상입니다. 가상 네트워크는 모든 hello 네트워크 보안 기능의 hello 기반 필수 tooestablish Azure에서 경계 네트워크 tooprotect 고객 배포 합니다.

## <a name="overview-of-azure-virtual-networks"></a>Azure Virtual Network 개요 
인터넷 트래픽을 toohello Azure 가상 네트워크를 가져올 수, 전에 보안 내재 된 toohello Azure 플랫폼의 두 계층 가지가 있습니다.

1.    **DDoS 방지**: DDoS 보호는 hello hello Azure 플랫폼 자체 대규모 인터넷 기반 공격 으로부터 보호 하는 실제 네트워크를 Azure의 계층입니다. 이러한 공격은 시도 toooverwhelm 인터넷 서비스의에서 여러 "bot" 노드를 사용합니다. Azure에는 모든 인바운드, 아웃바운드 및 Azure 지역 연결 간에 강력한 DDoS 방지 메시가 있습니다. 이 DDoS 보호 계층에는 사용자 구성 가능 특성이 없습니다 하며 액세스할 수 있는 toohello 고객 않습니다. 대규모 공격 으로부터 플랫폼으로 Azure를 보호 하는 hello DDoS 보호 계층, 아웃 바운드 트래픽을 캡슐화 된 트래픽과 크로스 Azure 영역의 또한 모니터링 합니다. 네트워크 가상 어플라이언스를 사용 하 여 hello VNet에, 추가 계층에 대 한 탄력성 hello 플랫폼 수준 보호 발생 하지 않는 보다 작은 눈금 공격 hello 고객별 구성할 수 있습니다. 작업에서 DDoS 예 경우에 인터넷 연결 IP 주소를 대규모 DDoS 공격에 의해 공격을 경우 Azure hello 공격 hello 소스를 인식 하 고 의도 한 대상에 도달 하기 전에 트래픽 잘못 된 hello를 제거 합니다. 거의 모든 경우에 hello 공격 받은 끝점 영향을 받지 않습니다 hello 공격입니다. 끝점의 영향을 받는다는 드문 경우 hello 트래픽이 영향을 받는 tooother 끝점, 공격 hello 끝점만입니다. 따라서 다른 고객 및 서비스는 해당 공격으로 인한 영향을 알지 못합니다. 것이 중요 한 toonote Azure DDoS 대규모 공격 검색만 하 합니다. Hello 플랫폼 수준 보호 임계값이 초과 되기 전에 특정 서비스에 너무 없습니다 것 같습니다. 예를 들어 Azure 플랫폼 수준 DDoS 보호에서 위협을 등록하기 전에 DDoS 공격에 의해 단일 A0 IIS 서버의 웹 사이트가 오프라인으로 사용될 수 있습니다.

2.  **공용 IP 주소**: 공용 IP 주소 (서비스 끝점, 공용 IP 주소, 응용 프로그램 게이트웨이 및 공용 IP 주소 toohello 인터넷 라우팅 tooyour 리소스를 제공 하는 다른 Azure 기능을 통해 사용 됨) 클라우드 서비스를 허용 또는 리소스 그룹의 toohave 공용 인터넷 IP 주소 및 노출 하는 포트입니다. hello 끝점이 hello Azure 가상 네트워크에 네트워크 주소 변환 (NAT) tooroute 트래픽 toohello 내부 주소와 포트를 사용합니다. 이 경로 hello 외부 트래픽이 toopass hello 가상 네트워크로에 대 한 기본 방법입니다. hello 공용 IP 주소 구성 가능한 toodetermine 트래픽을 전달 되며 방법과 위치 toohello 가상 네트워크에 변환 됩니다.

트래픽 hello 가상 네트워크에 도달 하면 고려해 야 하는 기능이 많이 있습니다. Azure 가상 네트워크의 작업량 및 기본 네트워크 수준 보안 적용 되는 고객 tooattach 하기 위한 기초 hello 됩니다. 중인 개인 네트워크 (가상 네트워크 오버레이) Azure hello 사용 하는 고객에 대 한 기능 및 특성이 다음:

* **트래픽 격리**: 가상 네트워크는 hello Azure 플랫폼에 hello 트래픽 격리 경계입니다. 하나의 가상 네트워크의 가상 컴퓨터 (Vm)에 다른 가상 네트워크에서 두 가상 네트워크를 만든 경우에 tooVMs hello 동일한 고객 직접 통신할 수 없습니다. 격리는 고객 VM과 통신이 가상 네트워크 안에서 비공개 상태를 유지하는 데 있어 중요한 속성입니다.

>[!NOTE]
>트래픽 격리 참조만 tootraffic *인바운드* toohello 가상 네트워크입니다. Hello VNet toohello의 아웃 바운드 트래픽이 기본적으로 인터넷은 허용 되지만 Nsg가 원하는 막을 수 있습니다.
>
>

* **다중 계층 토폴로지**: 가상 네트워크 내에서 고객 수 toodefine 다중 계층 토폴로지 서브넷에 할당 하 고 다양 한 요소 또는 해당 작업의 "계층"에 대 한 별도 주소 공간을 지정 하 여 합니다. 이러한 논리적 그룹 및 토폴로지 hello 작업 부하 유형을 기반으로 하는 고객 toodefine 서로 다른 액세스 정책을 사용 하 고 hello 계층 간 트래픽 흐름을 제어할 수도 있습니다.
* **크로스 프레미스 연결**: 고객은 Virtual Network와 다중 온-프레미스 사이트 간 또는 Azure의 다른 Virtual Network 간에 크로스 프레미스 연결을 설정할 수 있습니다. VNet 피어 링, Azure VPN 게이트웨이, 공급 업체 네트워크 가상 어플라이언스 또는 express 경로 연결 tooconstruct 고객을 사용할 수 있습니다. Azure는 표준 IPsec/IKE 프로토콜 및 Express 경로 개인 연결을 사용한 사이트 간(S2S) VPN을 지원합니다.
* **NSG** hello 원하는 수준의 세분성에서 고객 toocreate 규칙 (Acl)을 허용 합니다.: 네트워크 인터페이스, 개별 Vm 또는 가상 서브넷입니다. 고객은 허용 또는 거부 크로스-프레미스 연결을 통해 고객의 네트워크의 시스템에서 가상 네트워크 내에서 hello 작업 간의 통신 하 여 액세스를 제어 하거나 직접 인터넷 통신 수 있습니다.
* **UDR** 및 **IP 전달** 고객 가상 네트워크 내에서 다양 한 계층 간의 toodefine hello 통신 경로 허용 합니다. 고객은 보안 경계 정책 적용, 감사 및 검사를 위해 방화벽, IDS/IPS 및 기타 가상 어플라이언스를 배포하고 이러한 보안 어플라이언스를 통해 네트워크 트래픽을 라우팅할 수 있습니다.
* **네트워크 가상 어플라이언스** hello Azure Marketplace의에서: 방화벽, 부하 분산 장치, 및 ID/IP와 같은 보안 어플라이언스 hello Azure 마켓플레이스에서 사용 가능 하 고 VM 이미지 갤러리 hello 합니다. 고객이 각자의 가상 네트워크 내부 및의 보안 경계 (hello 경계 네트워크 서브넷 포함)는 다중 계층 toocomplete 안전한 네트워크 환경에 특히, 이러한 어플라이언스를 배포할 수 있습니다.

이러한 기능 및 기능 한 가지 예로 경계 네트워크 아키텍처를 Azure에서 구성할 수 있습니다 어떻게 다이어그램을 다음 hello 표시 됩니다.

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>경계 네트워크 특성 및 요구 사항
hello 경계 네트워크는 hello 프런트 엔드 hello 네트워크를 직접 조작 하는 hello 인터넷에서에서 통신 합니다. 들어오는 hello 패킷에 hello 백 엔드 서버에 도달 하기 전에 hello 방화벽, ID 및 ip 주소로 같은 hello 보안 어플라이언스를 통해 전달 합니다. Hello 워크 로드에서 인터넷에 바인딩된 패킷을 정책 적용, 검사 및 감사할 목적으로 hello 네트워크에서 없어지기 전에 hello 경계 네트워크에 hello 보안 어플라이언스를 통해 진행 될 수도 있습니다. 또한 hello 경계 네트워크는 고객 가상 네트워크와 온-프레미스 네트워크 간에 크로스-프레미스 VPN 게이트웨이 호스트할 수 있습니다.

### <a name="perimeter-network-characteristics"></a>경계 네트워크 특성
Hello 이전 그림을 참조 하는 뛰어난 경계 네트워크의 hello 특성 중 일부는 다음과 같습니다.

* 인터넷 연결:
  * 자체 hello 경계 네트워크 서브넷은 인터넷에 연결, 인터넷 hello와 직접 통신 합니다.
  * 공용 IP 주소, Vip 및/또는 서비스 끝점이 인터넷 트래픽 toohello 프런트 엔드 네트워크 및 장치를 전달합니다.
  * 트래픽 hello hello 프런트 엔드 네트워크에서 다른 리소스 하기 전에 보안 장치를 통해 전달 하는 인터넷에서에서 인바운드 합니다.
  * 아웃 바운드 보안을 사용 하는 경우 트래픽 toohello 인터넷 전달 하기 전에 보안 장치 hello 마지막 단계로, 통과 합니다.
* 보호되는 네트워크:
  * Hello 인터넷 toohello 핵심 인프라에서 직접 경로가 없습니다.
  * Nsg, 방화벽 또는 VPN 장치 등과 같은 보안 장치를 통해 채널 toohello 핵심 인프라를 트래버스해야 합니다.
  * 다른 장치 인터넷 및 hello 핵심 인프라를 브리징 해야 합니다.
  * 보안 장치 모두에 인터넷 hello 표시 되며 hello 경계 네트워크 (예를 들어 두 hello 방화벽 아이콘 hello 이전 그림에 표시)의 경계를 바라보 hello 보호 되는 네트워크 실제로 차별화 된 규칙으로 단일 가상 어플라이언스 또는 각 경계에 대 한 인터페이스입니다. 예를 들어 하나의 물리적 장치를 논리적으로 분리 되어 hello 경계 네트워크의 경계 둘 다에 대 한 hello 부하를 처리 합니다.
* 다른 일반적인 사례 및 제약 조건:
  * 워크로드는 업무상 중요 정보를 저장할 수 없음
  * 액세스 및 업데이트 tooperimeter 네트워크 구성 및 배포는 권한이 제한 된 tooonly 관리자입니다.

### <a name="perimeter-network-requirements"></a>경계 네트워크 요구 사항
tooenable 이러한 특성을 가상 네트워크 요구 사항 tooimplement 성공적인 경계 네트워크에 다음이 지침을 따릅니다.

* **서브넷 아키텍처:** 지정 hello 가상 네트워크 전체 서브넷 hello 경계 네트워크와 전용 되도록 구분 된 hello에서 다른 서브넷에서 동일한 가상 네트워크입니다. 이러한 분리는 hello 경계 네트워크 및 방화벽 또는 ID/IP는 가상 어플라이언스를 통해 다른 내부 또는 개인 서브넷 계층 흐름 간에 트래픽을 hello를 보장합니다.  서브넷은 hello 경계에서 사용자 정의 경로 tooforward이 트래픽을 toohello 가상 어플라이언스를 필요 합니다.
* **NSG:** 자체 hello 경계 네트워크 서브넷 hello 인터넷 열려 tooallow 통신할 수도 있지만 고객 Nsg를 무시 해야 의미는 아닙니다. 일반적인 보안 사례 toominimize hello 네트워크 노출 표면 toohello 인터넷을 따릅니다. Tooaccess hello 배포 또는 hello 특정 응용 프로그램 프로토콜 및 열려 있는 포트를 허용 하는 hello 원격 주소 범위 잠글 수 있습니다. 그러나 전체 잠금이 불가능한 환경이 있을 수 있습니다. 예를 들어 고객이 Azure에서 외부 웹 사이트를 사용할 경우 hello 경계 네트워크에서 공용 IP 주소를 hello 들어오는 웹 요청을 허용 해야 하지만 hello 웹 응용 프로그램 포트를 열어야: 포트 80에 TCP 및/또는 포트 443 TCP입니다.
* **라우팅 테이블:** 자체 hello 경계 네트워크 서브넷을 직접 수 toocommunicate toohello 인터넷 여야 하지만 직접 통신 tooand hello 백 엔드 또는 온-프레미스 네트워크에서 방화벽을 통해 이동 하지 않고도 허용 해서는 안 또는 보안 구성할 수 있습니다.
* **보안 어플라이언스 구성:** tooroute 및 hello 경계 네트워크와 hello 나머지 보호 hello 네트워크 간에 패킷을 검사, ID, 방화벽과 같은 보안 어플라이언스 hello 및 IP 장치 다중 홈이 될 수 있습니다. Hello 경계 네트워크 및 hello 백 엔드 서브넷에 대 한 별도 Nic 있을 수 있습니다. hello Nic hello 경계 네트워크에 직접 tooand hello 인터넷에서에서 통신, hello로 해당 Nsg hello 경계 네트워크 및 라우팅 테이블입니다. Nsg와 hello 해당 백 엔드 서브넷의 라우팅 테이블 toohello 백 엔드 서브넷에 연결 하는 hello Nic 제한 합니다.
* **보안 어플라이언스 기능:** 일반적으로 hello 경계 네트워크에 배포 된 hello 보안 어플라이언스 hello 다음 기능을 수행 합니다.
  * 방화벽: 방화벽 규칙 또는 hello 들어오는 요청에 대 한 액세스 제어 정책을 적용 합니다.
  * 위협 검색 및 방지: 검색 하 고 hello 인터넷에서에서 악의적인 공격을 완화 합니다.
  * 감사 및 로깅: 감사 및 분석을 위한 상세 로그 유지 관리합니다.
  * 역방향 프록시: toohello 해당 하는 백 엔드 서버가 요청 hello 들어오는 리디렉션. 이러한 리디렉션을 매핑 및 toohello 백 엔드 서버 주소 방화벽 일반적으로 hello 프런트 엔드 장치의 hello 대상 주소 변환 합니다.
  * 프록시를 전달: NAT를 제공 하 고 hello 가상 네트워크 toohello 인터넷 내부에서 시작 하는 통신에 대 한 감사를 수행 합니다.
  * 라우터: hello 가상 네트워크 내의 들어오고 서브넷 간 트래픽을 전달 합니다.
  * VPN 장치: hello 크로스-프레미스에 대 한 VPN 게이트웨이 작동 크로스-프레미스 고객 온-프레미스 네트워크와 Azure 가상 네트워크 간에 VPN 연결 합니다.
  * VPN 서버: tooAzure 가상 네트워크에 연결 하는 VPN 클라이언트를 수락 합니다.

> [!TIP]
> 다음 두 개의 그룹 별도 hello 유지: hello 개인 tooaccess hello 경계 네트워크 보안 기어 및 hello 권한이 있는 개인 응용 프로그램 개발, 배포 또는 작업 관리자 권한을 부여 합니다. 이 그룹을 별도로 유지하면 의무를 분리하고, 한 개인이 응용 프로그램 보안과 네트워크 보안 제어를 모두 무시하지 않도록 합니다.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>질문 toobe 네트워크 경계를 만들 때 요청
이 섹션에서는 구체적으로 언급 하지 않는 한 hello "네트워크" 이라는 용어는 tooprivate Azure 구독 관리자가 만든 가상 네트워크입니다. hello 용어 toohello Azure 내에서 기본 실제 네트워크를 참조 하지 않습니다.

또한 Azure 가상 네트워크는 자주 사용 되는 tooextend 기존의 온-프레미스 네트워크입니다. 가능한 tooincorporate는 사이트 간 또는 express 경로 하이브리드 네트워킹 경계 네트워크 아키텍처를 가진 솔루션 중 하나입니다. 이 하이브리드 링크는 네트워크 보안 경계를 구성할 때 고려해야 하는 중요한 요소입니다.

hello 다음 세 가지 질문은 중요 한 tooanswer 경계 네트워크와 여러 보안 경계를 사용 하 여 네트워크를 빌드하는 경우입니다.

#### <a name="1-how-many-boundaries-are-needed"></a>1) 필요한 경계 수는?
hello 첫 번째 의사 결정 점은 toodecide 개수 보안 경계가 지정된 된 시나리오에 필요 합니다.

* 단일 경계: hello 가상 네트워크와 인터넷 hello hello 프런트 엔드 경계 네트워크에 하나씩 있습니다.
* 두 경계: hello 경계 네트워크 서브넷과 백 엔드 서브넷에 hello 간에 다른 Azure 가상 네트워크를 hello 및 hello hello 경계 네트워크의 인터넷 쪽에 하나씩 있습니다.
* 세 가지 경계: hello 경계 네트워크의 인터넷 쪽 hello, hello 경계 네트워크 및 백 엔드 서브넷 간의 및 hello 백 엔드 서브넷과 hello 온-프레미스 네트워크 간의 합니다.
* N 경계 - 변수 번호입니다. 보안 요구 사항에 따라 제공된 된 네트워크에서 적용할 수 있는 보안 경계 수 없는 제한 toohello 있습니다.

hello 개수와 유형의 경계를 변경 하는 데 필요한 시나리오에 따라 회사의 위험 내결함성 및 hello 특정 구현 되 고 있습니다. 이 의사 결정은 종종 위험 및 규정 준수 팀, 네트워크와 플랫폼 팀, 응용 프로그램 개발 팀을 포함한 조직 내 여러 그룹이 함께 결정하는 사안입니다. 각 구현은이 의사 결정 tooensure hello 적절 한 보안 입장은 의견을 언급 해서도 기술, 관련 된 hello 데이터 보안과 hello 기술을 사용 하 고 있는 사용자가 있어야 합니다.

> [!TIP]
> 특정된 상황에 대 한 hello 보안 요구 사항을 충족 하는 경계의 hello 가장 작은 수를 사용 합니다. 자세한 경계와 운영 및 문제 해결 하기가 어려울 뿐만 수 시간이 지남에 따라 관리 hello 관리와 관련 된 오버 헤드를 여러 경계 정책을 hello 합니다. 그러나 경계가 불충분하면 위험이 커집니다. 찾기 hello 분산 하는 것이 중요 합니다.
>
>

![6]

hello 위의 그림은 높은 수준의 세 가지 보안 경계 네트워크입니다. hello 경계 hello 경계 네트워크 및 인터넷 hello, hello Azure 프런트 엔드 및 백 엔드 개인 서브넷 및 hello Azure 백 엔드 서브넷 및 hello 온-프레미스 회사 네트워크 간에입니다.

#### <a name="2-where-are-hello-boundaries-located"></a>2)는 hello 경계 어디에 있습니까?
Hello 경계 수를 결정 하는 한 후 tooimplement 하는 다음 의사 결정 지점을 hello 위치입니다. 일반적으로 3가지 선택 사항이 있습니다.

* 인터넷 기반 중개 서비스 사용(예: 클라우드 기반 웹 응용 프로그램 방화벽, 이 문서에서 논의하지 않음)
* Azure에서 기본 기능 및/또는 네트워크 가상 어플라이언스 사용
* Hello 온-프레미스 네트워크에서 물리적 장치를 사용 하 여

순수 하 게 Azure 네트워크에서 hello 옵션은 Azure에서 기본 기능 (예를 들어 Azure 부하 분산 장치) 또는에서 네트워크 가상 어플라이언스 hello (예: 검사점 방화벽) Azure의 다양 한 파트너 에코 시스템입니다.

Azure와 온-프레미스 네트워크 경계는 필요에 따라 hello 보안 장치 hello 연결 (또는 양쪽)의 어느 쪽에 있을 수 있습니다. 따라서 의사 결정 hello 위치 tooplace 보안 기어에서 수행 되어야 합니다.

Hello 인터넷-경계 네트워크와 hello 앞에 백 엔드 경계 Azure 내에서 완전히 포함 된 hello 위의 그림에서 및 네트워크 가상 어플라이언스 이거나 Azure에서 기본 기능 이어야 합니다. 보안 장치에서 Azure (백 엔드 서브넷) 사이의 경계 hello 및 hello Azure 측에서 또는 hello 온-프레미스 측 또는 양쪽 모두에서 장치의 조합 hello 회사 네트워크 일 수 있습니다. 중요 한 장점 및 단점 tooeither 옵션 심각 하 게 고려해 야 할 수 있습니다.

예를 들어 hello에서 기존 물리적 보안 장비를 사용 하 여 온-프레미스 네트워크 쪽 이점이 hello 없는 새 기어 필요 합니다. 재구성만 하면 됩니다. 그러나 hello, 단점은 모든 트래픽이 Azure toohello 온-프레미스 네트워크 toobe hello 보안 기어 볼에서 다시 가져와야 합니다. 따라서 Azure-Azure 트래픽 수 상당한 대기 시간을 부과 하 고 응용 프로그램 성능과 사용자 경험에 영향을, 백 toohello를 강제 적용 된 경우 온-프레미스 네트워크 보안 정책 적용에 대 한 합니다.

#### <a name="3-how-are-hello-boundaries-implemented"></a>Hello 경계 구현 하는 3) 방법
각 보안 경계가 서로 다른 기능 요구 사항 (예: ID 및 hello hello 경계 네트워크 및 백 엔드 서브넷 간에 Acl만 hello 경계 네트워크의 인터넷 쪽에 방화벽 규칙)에 있을 것입니다. 결정에 따라 달라 집니다 toouse 어떤 장치 (또는 장치 수) hello 시나리오 및 보안 요구 사항입니다. Hello 섹션 뒤, 1, 2 및 3 예제 사용 될 수 있는 몇 가지 옵션을 설명 합니다. Hello Azure 네이티브 네트워크 기능 및 hello 파트너 에코 시스템에서 Azure에서 사용할 수 있는 hello 장치 검토 거의 모든 시나리오 hello 수많은 옵션 사용 가능한 toosolve 표시 합니다.

또 다른 중요 한 구현 의사 결정 지점 어떻게 tooconnect hello 온-프레미스 Azure 사용 하 여 네트워크입니다. Azure 가상 게이트웨이 hello 또는 네트워크 가상 어플라이언스 언제 사용 하나요? 이러한 옵션은 다음 섹션 (예제 4, 5 및 6) hello에 더 자세히 설명 되어 있습니다.

또한 Azure 내부의 Virtual Network 간 트래픽이 필요할 수 있습니다. 이러한 시나리오는 hello 앞에 추가 됩니다.

위의 질문 toohello hello 답변을 알게 되 면 hello [빠른 시작](#fast-start) 섹션 통해는 예는 지정된 된 시나리오에 가장 적합 한 식별할 수 있습니다.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>예제: Azure Virtual Network와의 보안 경계 빌드
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Nsg와 응용 프로그램을 보호 하는 예 1 빌드 경계 네트워크 toohelp
[백업 tooFast 시작](#fast-start) | [Detailed 빌드이 예제에 대 한 지침][Example1]

[![7]][7]

#### <a name="environment-description"></a>환경 설명
이 예제에서는 hello 다음 리소스를 포함 하는 구독이입니다.

- 단일 리소스 그룹
- 두 서브넷 "프런트 엔드" 및 "백 엔드"를 사용하는 가상 네트워크
- 적용 된 tooboth 서브넷은 네트워크 보안 그룹
- 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
- 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
- DNS 서버("DNS01")를 나타내는 Windows Server
- Hello 응용 프로그램 웹 서버와 관련 된 공용 IP

스크립트 및 Azure 리소스 관리자 템플릿을 참조 hello [빌드 방법을 자세히 설명][Example1]합니다.

#### <a name="nsg-description"></a>NSG 설명
이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.

> [!TIP]
> 일반적으로 특정 "Allow" 규칙 먼저 만들어야, 보다 일반적인 hello 이어서 "거부" 규칙입니다. 우선 순위를 지정 하는 hello는 규칙이 먼저 평가 지정 합니다. 트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다. NSG 규칙에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향 hello 중 하나입니다.
>
>

선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:

1. 내부 DNS 트래픽(포트 53)이 허용됩니다.
2. RDP 트래픽 (포트 3389 hello 인터넷 tooany 가상 컴퓨터에서 에서) 허용 됩니다.
3. Hello 인터넷 tooweb 서버 (IIS01)에서 HTTP 트래픽 (포트 80)가 허용 됩니다.
4. (모든 포트) IIS01 tooAppVM1에서 모든 트래픽이 허용 됩니다.
5. Hello 인터넷 toohello 전체 가상 네트워크 (서브넷 모두)에서 모든 트래픽 (모든 포트) 거부 되었습니다.
6. Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.

이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청 hello 인터넷 toohello 웹 서버 로부터 언바운드 하지 않은 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것입니다. 규칙 3이 우선 순위가 높기 때문에 규칙 3만 적용되고 규칙 5는 진행되지 않습니다. 따라서 toohello 웹 서버 hello HTTP 요청 허용 합니다. 동일한 트래픽이 해당 tooreach DNS01 hello 서버를 시도 하 고, 규칙을 5 (거부)는 첫 번째 tooapply hello 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 될 수 있습니다. 규칙 6 블록 hello 통하게 (규칙 1 및 4에서에서 허용 된 트래픽)를 제외한 toohello 백 엔드 서브넷에서 프런트 엔드 서브넷 (거부) 합니다. 이 규칙 집합 공격자 hello 프런트 엔드에 hello 웹 응용 프로그램 성능을 저하 하는 경우 hello 백 엔드 네트워크를 보호 합니다. hello 공격자가 제한 될 수 toohello 백 엔드 "보호" 네트워크 액세스 (만 tooresources hello AppVM01 서버에서 노출).

Toohello 인터넷으로 트래픽을 허용 하는 기본 아웃 바운드 규칙이 있습니다. 이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다. 양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅을 필요 (예 3 참조).

#### <a name="conclusion"></a>결론
이 예제는 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 간단 하 고 간단한 방법입니다. 자세한 내용은 참조 hello [빌드 방법을 자세히 설명][Example1]합니다. 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이이 경계 네트워크 클래식 PowerShell 스크립트입니다.
* 어떻게 toobuild이이 경계 네트워크는 Azure 리소스 관리자 템플릿을 사용 하 여 합니다.
* 각 NSG 명령에 대한 상세 설명
* 각 계층에서의 트래픽 허용 또는 거부 방법을 나타내는 상세 트래픽 흐름 시나리오입니다.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>예제 2 빌드 경계 네트워크 toohelp 방화벽 Nsg와 응용 프로그램을 보호
[백업 tooFast 시작](#fast-start) | [Detailed 빌드이 예제에 대 한 지침][Example2]

[![8]][8]

#### <a name="environment-description"></a>환경 설명
이 예제에서는 hello 다음 리소스를 포함 하는 구독이입니다.

* 단일 리소스 그룹
* 두 서브넷 "프런트 엔드" 및 "백 엔드"를 사용하는 가상 네트워크
* 적용 된 tooboth 서브넷은 네트워크 보안 그룹
* 이 경우에는 방화벽에서 네트워크 가상 어플라이언스 toohello 프런트 엔드 서브넷 연결
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server

스크립트 및 Azure 리소스 관리자 템플릿을 참조 hello [빌드 방법을 자세히 설명][Example2]합니다.

#### <a name="nsg-description"></a>NSG 설명
이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.

> [!TIP]
> 일반적으로 특정 "Allow" 규칙 먼저 만들어야, 보다 일반적인 hello 이어서 "거부" 규칙입니다. 우선 순위를 지정 하는 hello는 규칙이 먼저 평가 지정 합니다. 트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다. NSG 규칙에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향 hello 중 하나입니다.
>
>

선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:

1. 내부 DNS 트래픽(포트 53)이 허용됩니다.
2. RDP 트래픽 (포트 3389 hello 인터넷 tooany 가상 컴퓨터에서 에서) 허용 됩니다.
3. 모든 인터넷 트래픽에 (모든 포트) toohello 네트워크 가상 어플라이언스 (방화벽)가 허용 됩니다.
4. (모든 포트) IIS01 tooAppVM1에서 모든 트래픽이 허용 됩니다.
5. Hello 인터넷 toohello 전체 가상 네트워크 (서브넷 모두)에서 모든 트래픽 (모든 포트) 거부 되었습니다.
6. Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.

이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청에 바인딩된 hello 인터넷 toohello 방화벽에서 한 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것입니다. 규칙 3이 우선 순위가 높기 때문에 규칙 3만 적용되고 규칙 5는 진행되지 않습니다. 따라서 toohello 방화벽 hello HTTP 요청 허용 합니다. 동일한 트래픽이 해당가 시도 하는 경우 tooreach hello IIS01 서버 hello 프런트 엔드 서브넷에도, 규칙 5 (거부) 적용 하는 것을 hello 트래픽 toopass toohello 서버 허용 되지 않는 한 합니다. 규칙 6 블록 hello 통하게 (규칙 1 및 4에서에서 허용 된 트래픽)를 제외한 toohello 백 엔드 서브넷에서 프런트 엔드 서브넷 (거부) 합니다. 이 규칙 집합 공격자 hello 프런트 엔드에 hello 웹 응용 프로그램 성능을 저하 하는 경우 hello 백 엔드 네트워크를 보호 합니다. hello 공격자가 제한 될 수 toohello 백 엔드 "보호" 네트워크 액세스 (만 tooresources hello AppVM01 서버에서 노출).

Toohello 인터넷으로 트래픽을 허용 하는 기본 아웃 바운드 규칙이 있습니다. 이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다. 양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅을 필요 (예 3 참조).

#### <a name="firewall-rule-description"></a>방화벽 규칙 설명
Hello 방화벽에서 전달 규칙 만들어야 합니다. 규칙은이 예제에서는 유일한 경로 인터넷 트래픽 인바운드 toohello 방화벽 및 전달 하나만 다음 toohello 웹 서버, 네트워크 주소 변환 (NAT) 하므로 필요 합니다.

규칙을 전달 하는 hello tooreach HTTP (포트 80 또는 443을 HTTPS)을 시도 하는 hello 방화벽에 접속 하는 모든 인바운드 소스 주소를 허용 합니다. Hello 방화벽의 로컬 인터페이스 다르게 전송 있으며 toohello 웹 서버 hello 10.0.1.5의 IP 주소로 리디렉션됩니다.

#### <a name="conclusion"></a>결론
이 예제는 비교적 간단한 방법 방화벽 응용 프로그램을 보호 하 고 hello 백 엔드 서브넷 인바운드 트래픽에서 격리입니다. 자세한 내용은 참조 hello [빌드 방법을 자세히 설명][Example2]합니다. 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이이 경계 네트워크 클래식 PowerShell 스크립트입니다.
* 어떻게 toobuild Azure 리소스 관리자 템플릿 사용 하 여이 예제입니다.
* 각 NSG 명령 및 방화벽 규칙에 대한 상세 설명
* 각 계층에서의 트래픽 허용 또는 거부 방법을 나타내는 상세 트래픽 흐름 시나리오입니다.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>예제 3 빌드 경계 네트워크 toohelp 방화벽 및 UDR NSG는 네트워크를 보호 합니다.
[백업 tooFast 시작](#fast-start) | [Detailed 빌드이 예제에 대 한 지침][Example3]

[![9]][9]

#### <a name="environment-description"></a>환경 설명
이 예제에서는 hello 다음 리소스를 포함 하는 구독이입니다.

* 단일 리소스 그룹
* "SecNet", "FrontEnd", "BackEnd"의 세 서브넷을 포함하는 가상 네트워크
* 이 경우에는 방화벽에서 네트워크 가상 어플라이언스 toohello SecNet 서브넷 연결
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server

스크립트 및 Azure 리소스 관리자 템플릿을 참조 hello [빌드 방법을 자세히 설명][Example3]합니다.

#### <a name="udr-description"></a>UDR 설명
기본적으로 시스템 경로 따라 hello로 정의 됩니다.

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

hello VNETLocal hello 해당 특정 네트워크에 대 한 가상 네트워크를 구성 하는 하나 이상의 정의 된 주소 접두사는 항상 (즉, 변경 각 특정 가상 네트워크를 정의 하는 방법에 따라 가상 네트워크 toovirtual 네트워크에서). 이 정적이 고 hello 표에 명시 되어 있는 대로 기본 hello 나머지 시스템 경로입니다.

이 예제에서는 두 개의 라우팅 테이블이 만들어진 hello 프런트 엔드 및 백 엔드 서브넷에 대해 각각 하나씩 있습니다. 각 테이블은 서브넷을 지정 하는 hello에 대 한 적절 한 고정 경로로 로드 됩니다. 이 예제에서는 각 테이블에는 모든 트래픽을 (0.0.0.0/0) 하는 세 가지 경로의 hello 방화벽을 통해 (다음 홉 = 가상 어플라이언스 IP 주소):

1. 다음 홉으로 로컬 서브넷 트래픽을 tooallow 로컬 서브넷 트래픽을 toobypass hello 방화벽을 정의 합니다.
2. 다음 홉이 방화벽으로 정의된 가상 네트워크 트래픽입니다. 다음 홉이 로컬 가상 네트워크 트래픽 tooroute를 직접 허용 하는 hello 기본 규칙을 재정의 합니다.
3. 다음 홉 hello 방화벽으로 정의 된 모든 나머지 트래픽 (0/0).

> [!TIP]
> Hello UDR 나누기 로컬 서브넷 통신에에서 hello 로컬 서브넷 항목을 포함 하지입니다.
>
> * 이 예제에서 tooVNETLocal 가리키는 10.0.1.0/24는 중요 한! 없으면 toohello NVA 전송 됩니다 hello 대상이 지정 되었으며 웹 서버 (10.0.1.4) tooanother 로컬 서버 (예) 10.0.1.25 두면 패킷 실패 합니다. hello NVA에서 것 toohello 서브넷 보내고 hello 서브넷 toohello NVA 무한 루프에 다시 됩니다.
> * hello 라우팅 루프가 발생할 가능성이 기존의 온-프레미스 어플라이언스의 자주 변경 되는 연결 된 tooseparate 서브넷에 있는 여러 개의 Nic와 어플라이언스에서 더 높습니다.
>
>

Hello 라우팅 테이블을 만든 후 바인딩된 tootheir 서브넷 이어야 합니다. 라우팅 테이블 프런트 엔드 서브넷 hello, 만든 and toohello 서브넷 바인딩된,이 출력은 같습니다.

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR 적용된 toohello 게이트웨이 서브넷이 있는 hello ExpressRoute 회로 연결 되어 될 수 있습니다.
>
> 예 3 및 4에에서 어떻게 tooenable 주변은 express 경로 또는 사이트 간 네트워킹을 네트워크의 예가 나와 있습니다.
>
>

#### <a name="ip-forwarding-description"></a>IP 전달 설명
도우미 기능 tooUDR은 IP 전달 합니다. IP 전달은 tooreceive 트래픽을 명시적으로 toohello 기기에서 허용 하 고 다음 해당 트래픽을 tooits 최종 대상으로 전달 하는 가상 어플라이언스 설정입니다.

예를 들어 AppVM01 toohello DNS01 서버 요청을 만드는 경우 UDR toohello 방화벽을이 트래픽을 라우팅합니다. IP 전달을 사용 하도록 설정와 hello DNS01 대상 (10.0.2.4)에 대 한 hello 트래픽은 hello 기기 (10.0.0.4)에서 허용 되 고 tooits 최종 대상 (10.0.2.4)를 전달 합니다. 없이 IP 전달 hello 방화벽에서 사용 하도록 설정, 트래픽 것에서 허용 되지 hello 기기 hello 경로 테이블에 hello 다음 홉으로 hello 방화벽이 있는 경우에 합니다. 가상 어플라이언스 toouse 것이 중요 한 tooremember tooenable IP UDR 함께 전달 합니다.

#### <a name="nsg-description"></a>NSG 설명
이 예제에서는 NSG 그룹을 빌드한 후 단일 규칙을 로드합니다. 이 그룹은 다음 toohello 프런트 엔드 및 백 엔드 서브넷만 (하지 SecNet hello)를 연결 합니다. 선언적 규칙을 따르는 hello 작성 중인:

* Hello 인터넷 toohello 전체 가상 네트워크 (모든 서브넷)에서 모든 트래픽 (모든 포트) 거부 되었습니다.

이 예제에서 NSG를 사용했지만 기본 목적은 수동 구성 시 실수가 발생할 경우를 대비하여 두 번째 방어 계층을 만드는 것입니다. hello ´ ֲ tooblock의 모든 인바운드 트래픽이 hello 인터넷 tooeither hello 프런트 엔드 또는 백 엔드 서브넷입니다. Hello SecNet 서브넷 toohello 방화벽을 통해 트래픽 흐름만 (그리고 toohello 프런트 엔드 또는 백 엔드 서브넷에 해당 하는 경우). 또한 장소에 hello UDR 규칙과 함께 않은 쉽게 변환할 hello 프런트 엔드 또는 백 엔드 서브넷 하는 모든 트래픽은 전송 toohello 방화벽 (감사 tooUDR) 초과 합니다. hello 방화벽 비대칭 흐름으로이 트래픽을 볼 수 있으며 hello 아웃 바운드 트래픽을 삭제 합니다. 따라서 hello 서브넷을 보호 하는 보안 계층 세 가지가 있습니다.

* FrontEnd 또는 BackEnd NIC에는 공용 IP 주소가 없습니다.
* Nsg hello 인터넷에서에서 트래픽을 거부 합니다.
* hello 방화벽 삭제 비대칭 트래픽입니다.

이 예에서 NSG hello에 대 한 흥미로운 사항이 하나는 toodeny 인터넷 트래픽을 toohello 전체 가상 네트워크를 hello 보안 서브넷을 포함 하 여 규칙이 하나만 포함 되어 있는 것입니다. 그러나 NSG는만 hello 바인딩된 toohello 프런트 엔드 및 백 엔드 서브넷 hello 규칙 트래픽에서 처리 되지 않습니다 하므로 인바운드 toohello 보안 서브넷입니다. 결과적으로 트래픽 흐름 toohello 보안 서브넷을 사용 합니다.

#### <a name="firewall-rules"></a>방화벽 규칙
Hello 방화벽에서 전달 규칙 만들어야 합니다. Hello 방화벽 차단 또는 모든 인바운드, 아웃 바운드 전달 및 내 가상 네트워크 트래픽을 이므로, 많은 방화벽 규칙이 필요 합니다. 또한 모든 인바운드 트래픽 도달 hello 보안 서비스 공용 IP 주소 (서로 다른 포트의 경우)에서 toobe hello 방화벽에 의해 처리 됩니다. 가장 좋은 방법은 toodiagram hello 서브넷을 설정 하기 전에 hello 논리 흐름 및 방화벽 규칙을 tooavoid 나중에 다시 작업 합니다. hello 다음 그림은이 예제에 대 한 hello 방화벽 규칙의 논리적 보기:

![10]

> [!NOTE]
> Hello 관리 포트에 사용 되는 네트워크 가상 어플라이언스 hello에 따라 다릅니다. 이 예제에서는 포트 22, 801, 807을 사용하는 Barracuda NextGen 방화벽을 참조합니다. Hello 어플라이언스 공급 업체 설명서 toofind hello 정확 하 게 사용 되는 포트를 사용 중인 hello 장치 관리를 참조 하십시오.
>
>

#### <a name="firewall-rules-description"></a>방화벽 규칙 설명
Hello 앞에 논리 다이어그램에서 hello 보안 서브넷 hello 방화벽은 해당 서브넷에만 리소스 hello 때문에 표시 되지 않습니다. hello 방화벽 규칙 및 방법은 논리적으로 허용 하거나 거부할 트래픽 흐름을 hello 실제 라우트된 경로가 아닌 hello 다이어그램이 표시 됩니다. 또한 hello RDP 트래픽이 높은 범위가 지정 된 포트 (8014 – 8026) 되며 hello로 정렬 된 선택한 tooloosely에 대해 선택 하는 hello 외부 포트 마지막 두 개 8 진수가 동일한 hello 쉽게 가독성을 위해 로컬 IP 주소 (예를 들어 로컬 서버 주소 10.0.1.4 연관 된 외부 포트와 8014). 하지만 이보다 높으면서 충돌하지 않는 포트도 사용할 수 있습니다.

이 예제에서는 7가지 유형의 규칙이 필요합니다.

* 외부 규칙(인바운드 트래픽용):
  1. 방화벽 관리 규칙:이 응용 프로그램 리디렉션 규칙이 트래픽 toopass hello 네트워크 가상 어플라이언스의 toohello 관리 포트를 허용 합니다.
  2. (각 Windows server) 용 RDP 규칙: (각 서버 마다 하나씩) 이러한 4 가지 규칙 RDP 통해 개별 서버 hello에서 관리할 수 있습니다. hello 네 개의 RDP 규칙 사용 중인 hello 네트워크 가상 어플라이언스의 hello 기능에 따라 하나의 규칙으로 축소도 수 없습니다.
  3. 응용 프로그램 트래픽 규칙: 이러한 규칙, hello 프런트 엔드 웹 트래픽에 대해 먼저 hello 및 hello 백 엔드 트래픽 (예를 들어 웹 서버 toodata 계층)에 대 한 두 번째 hello의 두 가지입니다. 이러한 규칙의 hello 구성 (서버 배치) hello 네트워크 아키텍처 및 트래픽 흐름 (어떤 방향이 hello 트래픽 흐름 및 사용 되는 포트)에 따라 다릅니다.
     * 첫 번째 규칙의 hello hello 실제 응용 프로그램 트래픽 tooreach hello 응용 프로그램 서버를 수 있습니다. Hello 다른 규칙에서는 보안 및 관리 하는 동안에 응용 프로그램 트래픽 규칙은 어떤 hello 응용 프로그램 외부의 사용자 또는 서비스 tooaccess입니다. 이 예제에서는 포트 80에 단일 웹 서버가 있습니다. 따라서 단일 응용 프로그램 ॉ 인바운드 트래픽을 toohello 외부 IP을 toohello 웹 서버의 내부 IP 주소를 리디렉션합니다. hello 리디렉션 트래픽 세션 NAT toohello 내부 서버를 통해 변환 합니다.
     * hello 두 번째 규칙 모든 포트를 통해 hello 백 엔드 규칙 tooallow hello 웹 서버 tootalk toohello AppVM01 서버 (않음 하지 AppVM02)입니다.
* 내부 규칙(Virtual Network 내부 트래픽용)
  1. 아웃 바운드 tooInternet 규칙:이 규칙은 toopass toohello 선택한 네트워크 모든 네트워크에서 트래픽을 허용 합니다. 이 규칙은 일반적으로 기본 규칙 요소가 hello 방화벽에 있지만 사용할 수 없는 상태에 있습니다. 이 예제에서는 이 규칙을 사용하도록 설정해야 합니다.
  2. DNS 규칙:이 규칙은 DNS (포트 53) 트래픽 toopass toohello DNS 서버 에서만 허용 됩니다. 이 환경에 대 한 hello 프런트 엔드 toohello 백 엔드에서 대부분 트래픽이 차단 됩니다. 이 규칙은 로컬 서브넷의 DNS만 특별히 허용합니다.
  3. 서브넷 toosubnet 규칙:이 규칙은 tooallow hello 프런트 엔드 서브넷 (역방향 hello 하지)에 백 엔드 서브넷 tooconnect tooany 서버 hello에서 모든 서버입니다.
* 유사 시 대기 (트래픽에 대 한 규칙 hello 이전 중 하나를 만족 하지 않는):
  1. 모든 트래픽 규칙 거부:이 거부 규칙 항상 hello 최종 규칙 (측면에서 우선 순위) 이어야 하며 따라서 트래픽 흐름에 실패 하면 toomatch hello 규칙 앞에 오는 경우 삭제 된이 규칙에 의해 합니다. 이 규칙은 기본 규칙으로 일반적으로 준비 및 활성화되어 있습니다. 수정할 수 없습니다는 일반적으로 필요한 toothis 규칙입니다.

> [!TIP]
> Hello에 두 번째 응용 프로그램 트래픽 규칙을 toosimplify이이 예제에서는 모든 포트가 허용 됩니다. 실제 시나리오에서는 hello 가장 구체적인 포트와 주소 범위는이 규칙의 사용된 tooreduce hello 공격 노출 되어야 합니다.
>
>

Hello 이전 규칙을 만든 후에 tooreview hello 각 규칙 tooensure 트래픽의 우선 순위 허용 또는 거부할지 필요에 따라 중요 합니다. 예를 들어 hello 규칙은 우선 순위에 따라입니다.

#### <a name="conclusion"></a>결론
이 예제는 더 복잡 한 않음 방식으로 보호 하 고 이전 예제 hello 보다 hello 네트워크 격리를 완료 합니다. (방금 hello 응용 프로그램을 보호 하는 예제 2 및 서브넷을 바로 격리 하는 예 1). 이 설계는 양방향으로 트래픽을 모니터링에 대 한 허용 및 뿐 아니라 hello 인바운드 응용 프로그램 서버를 보호 하지만이 네트워크에 있는 모든 서버에 대 한 네트워크 보안 정책을 적용 합니다. 또한 hello 어플라이언스에 사용에 따라 전체 트래픽 감사 및 인식을 수행할 수 있습니다. 자세한 내용은 참조 hello [빌드 방법을 자세히 설명][Example3]합니다. 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이 예제에서는 경계 네트워크 클래식 PowerShell 스크립트입니다.
* 어떻게 toobuild Azure 리소스 관리자 템플릿 사용 하 여이 예제입니다.
* 각 UDR, NSG 명령 및 방화벽 규칙에 대한 상세 설명입니다.
* 각 계층에서의 트래픽 허용 또는 거부 방법을 나타내는 상세 트래픽 흐름 시나리오입니다.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>예 4 사이트 간, 가상 어플라이언스 VPN에 하이브리드 연결 추가
[백업 tooFast 시작](#fast-start) | 곧 사용할 수 있는 빌드 방법을 자세히 설명

[![11]][11]

#### <a name="environment-description"></a>환경 설명
하이브리드 네트워킹 (NVA) 네트워크 가상 어플라이언스를 사용 하 여 1, 2 또는 3 예제에 설명 된 hello 경계 네트워크 유형의 tooany를 추가할 수 있습니다.

Hello 이전 그림에 표시 된 것과 같이 hello (사이트-사이트) 인터넷을 통한 VPN 연결이 사용 되는 tooconnect NVA 통해 Azure 가상 네트워크는 온-프레미스 네트워크 tooan 것입니다.

> [!NOTE]
> ExpressRoute를 사용 하 여 hello Azure 공용 피어 링 옵션을 설정 하는 경우 고정 경로 만들어야 합니다. 이 고정 경로 toohello hello ExpressRoute 연결을 통해서가 아니라 회사 인터넷 아웃 NVA VPN IP 주소 라우팅해야 합니다. hello hello ExpressRoute Azure 공용 피어 링 옵션에 필요한 NAT hello VPN 세션을 중단 될 수 있습니다.
>
>

VPN 설정 되 고 hello hello NVA 모든 네트워크 및 서브넷에 대 한 중앙 허브 hello 됩니다. hello 방화벽 전달 규칙에는 어떤 트래픽 흐름이 허용 됩니다 NAT을 통해 변환, 리디렉션되는 또는 (hello 온-프레미스 네트워크와 Azure 간의 트래픽 흐름)에 삭제 됩니다 결정 합니다.

최적화 될 수 있습니다 또는 사용 특정 hello에 따라이 디자인 패턴에서 성능 저하 사례 때 트래픽 흐름을 신중 하 게 고려 되어야 합니다.

예제 3, 기본 제공 hello 환경을 사용 하 고 다음 추가 사이트 간 VPN 하이브리드 네트워크 연결을 디자인 하는 hello을 생성 합니다.

[![12]][12]

hello 온-프레미스 라우터 또는 사용자 NVA VPN에 대 한 호환 되는 기타 네트워크 장치는 VPN 클라이언트 hello 것입니다. 이 물리적 장치를 시작 하 고 프로그램 NVA와 hello VPN 연결을 유지 관리 담당 것입니다.

논리적으로 NVA toohello hello 네트워크 상태에 네 개의 개별 "보안 영역" hello 규칙 hello NVA 있는 것에 이러한 영역 간의 트래픽 기본 디렉터 hello:

![13]

#### <a name="conclusion"></a>결론
사이트 간 VPN 하이브리드 네트워크 연결 tooan Azure 가상 네트워크의 hello 추가 안전한 방식으로 Azure로 hello 온-프레미스 네트워크를 확장할 수 있습니다. VPN 연결을 사용 하 여 트래픽을 암호화 되 고 라우팅합니다 hello 인터넷을 통해. 이 예에서 NVA hello 중앙 위치 tooenforce를 제공 하며 hello 보안 정책을 관리 합니다. 자세한 내용은 자세한 hello를 참조 하세요. 빌드 지침 (곧 출시 예정인). 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이 예제에서는 경계 네트워크와 PowerShell 스크립트입니다.
* 어떻게 toobuild Azure 리소스 관리자 템플릿 사용 하 여이 예제입니다.
* 이 설계에서의 트래픽 흐름을 보여 주는 상세 트래픽 흐름 시나리오입니다.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>예제 5 사이트 간 Azure VPN Gateway를 통한 하이브리드 연결 추가
[백업 tooFast 시작](#fast-start) | 곧 사용할 수 있는 빌드 방법을 자세히 설명

[![14]][14]

#### <a name="environment-description"></a>환경 설명
Azure VPN 게이트웨이 사용 하 여 하이브리드 네트워킹 예제 1 또는 2에에서 설명 된 tooeither 경계 네트워크 형식을 추가할 수 있습니다.

Hello 그림 앞에 표시 된 것과 같이 hello (사이트-사이트) 인터넷을 통한 VPN 연결은 Azure VPN 게이트웨이 통해 Azure 가상 네트워크는 온-프레미스 네트워크 tooan tooconnect를 사용 하는 것입니다.

> [!NOTE]
> ExpressRoute를 사용 하 여 hello Azure 공용 피어 링 옵션을 설정 하는 경우 고정 경로 만들어야 합니다. 이 고정 경로 toohello hello ExpressRoute WAN을 통해서가 아니라 회사 인터넷 아웃 NVA VPN IP 주소 라우팅해야 합니다. hello hello ExpressRoute Azure 공용 피어 링 옵션에 필요한 NAT hello VPN 세션을 중단 될 수 있습니다.
>
>

hello 다음 그림은 hello 두 네트워크 가장자리가 예제. Hello 첫 번째 가장자리에 NVA hello 및 Nsg 방법은 Azure 네트워크에 대 한와 Azure 간의 트래픽 흐름을 제어 하 고 인터넷 hello 합니다. hello 두 번째 가장자리가 hello Azure VPN 게이트웨이 온-프레미스와 Azure 간 별도 및 격리 된 네트워크 가장자리입니다.

최적화 될 수 있습니다 또는 사용 특정 hello에 따라이 디자인 패턴에서 성능 저하 사례 때 트래픽 흐름을 신중 하 게 고려 되어야 합니다.

예 1, 기본 제공 hello 환경을 사용 하 고 다음 추가 사이트 간 VPN 하이브리드 네트워크 연결을 디자인 하는 hello을 생성 합니다.

[![15]][15]

#### <a name="conclusion"></a>결론
사이트 간 VPN 하이브리드 네트워크 연결 tooan Azure 가상 네트워크의 hello 추가 안전한 방식으로 Azure로 hello 온-프레미스 네트워크를 확장할 수 있습니다. Hello 기본 Azure VPN 게이트웨이 사용 하 여 트래픽을 IPSec 암호화 이며 hello 인터넷을 통해 라우팅합니다. 또한 hello Azure VPN 게이트웨이 사용 하 여 필요한 저렴 한 비용 옵션 (추가 라이센스가 제 3 자 NVAs와 마찬가지로 비용)을 제공할 수 있습니다. 이 옵션은 NVA를 사용하지 않는 예제 1에서는 가장 경제적입니다. 자세한 내용은 자세한 hello를 참조 하세요. 빌드 지침 (곧 출시 예정인). 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이 예제에서는 경계 네트워크와 PowerShell 스크립트입니다.
* 어떻게 toobuild Azure 리소스 관리자 템플릿 사용 하 여이 예제입니다.
* 이 설계에서의 트래픽 흐름을 보여 주는 상세 트래픽 흐름 시나리오입니다.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>예제 6 ExpressRoute를 통한 하이브리드 연결 추가
[백업 tooFast 시작](#fast-start) | 곧 사용할 수 있는 빌드 방법을 자세히 설명

[![16]][16]

#### <a name="environment-description"></a>환경 설명
개인 피어 링 연결 될 수 있습니다는 ExpressRoute를 사용 하 여 하이브리드 네트워킹 예제 1 또는 2에에서 설명 된 tooeither 경계 네트워크 형식을 추가 합니다.

Hello 앞 그림 에서처럼 개인 피어 링 express 경로 hello Azure 가상 네트워크 및 온-프레미스 네트워크 간의 직접 연결을 제공 합니다. 트래픽은 hello 서비스 공급자 네트워크 및 인터넷 hello을 터치 하지 hello Microsoft Azure 네트워크를 자신입니다.

> [!TIP]
> ExpressRoute를 사용 하 여 회사 네트워크 트래픽을 hello 인터넷 오프은 유지 합니다. Express 공급자로부터의 Service Level Agreements(서비스 수준 약정)도 허용됩니다. hello Azure 게이트웨이 사이트 간 Vpn과 hello Azure 게이트웨이 최대 처리량은 200mbps 반면 ExpressRoute 사용 too10 g b p s를 전달할 수 있습니다.
>
>

Hello 다음 다이어그램에서에서와 같이이 옵션 hello로 환경에 네트워크 가장자리를 두 개 있습니다. hello NVA 및 NSG 제어 트래픽 흐름 및 Azure와 hello 인터넷 hello 게이트웨이 온-프레미스와 Azure 간 별도 및 격리 된 네트워크 경계 내 Azure 네트워크에 대 한 합니다.

최적화 될 수 있습니다 또는 사용 특정 hello에 따라이 디자인 패턴에서 성능 저하 사례 때 트래픽 흐름을 신중 하 게 고려 되어야 합니다.

한 다음 ExpressRoute 하이브리드 네트워크 연결을 추가 하는 예 1 작성 하는 hello 환경을 사용 하 여 hello 디자인을 생성 합니다.

[![17]][17]

#### <a name="conclusion"></a>결론
ExpressRoute 개인 피어 링 네트워크 연결의 hello 추가 확장할 수 있습니다 hello 온-프레미스 네트워크를 Azure로 안전 하 고 더 낮은 대기 시간, 높은 방식으로 수행 합니다. 이 예제와 같이 네이티브 Azure 게이트웨이 (더 추가 제 3 자 NVAs와 마찬가지로 라이선스)는 필요한 저렴 한 비용 옵션을 제공 하는 또한 hello를 사용 하 여 합니다. 자세한 내용은 자세한 hello를 참조 하세요. 빌드 지침 (곧 출시 예정인). 이러한 지침에는 다음이 포함됩니다.

* 어떻게 toobuild이 예제에서는 경계 네트워크와 PowerShell 스크립트입니다.
* 어떻게 toobuild Azure 리소스 관리자 템플릿 사용 하 여이 예제입니다.
* 이 설계에서의 트래픽 흐름을 보여 주는 상세 트래픽 흐름 시나리오입니다.

## <a name="references"></a>참조
### <a name="helpful-websites-and-documentation"></a>유용한 웹 사이트 및 설명서
* Azure Resource Manager를 사용한 Azure 액세스:
* PowerShell을 통한 Azure 액세스: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* 가상 네트워킹 설명서: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* 네트워크 보안 그룹 설명서: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* 사용자 정의 라우팅 설명서: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Azure 가상 게이트웨이: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* 사이트 간 VPN: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Express 경로 설명서 (hello "시작" 및 "How To" 섹션 아웃 있는지 toocheck 수): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "보안 옵션 순서도"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Azure 보안 기능"
[3]: ./media/best-practices-network-security/dmzcorporate.png "회사 네트워크의 DMZ"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Azure 보안 아키텍처"
[5]: ./media/best-practices-network-security/dmzazure.png "Azure Virtual Network의 DMZ"
[6]: ./media/best-practices-network-security/dmzhybrid.png "3개의 보안 경계가 있는 하이브리드 네트워크"
[7]: ./media/best-practices-network-security/example1design.png "NSG와 인바운드 DMZ"
[8]: ./media/best-practices-network-security/example2design.png "NVA 및 NSG와 인바운드 DMZ"
[9]: ./media/best-practices-network-security/example3design.png "NVA, NSG, UDR을 사용하는 양방향 DMZ"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "hello 방화벽 규칙의 논리적 보기"
[11]: ./media/best-practices-network-security/example3designoptions.png "NVA 연결 하이브리드 네트워크가 있는 DMZ"
[12]: ./media/best-practices-network-security/example4designs2s.png "사이트 간 VPN을 통해 연결된 NVA가 있는 DMZ"
[13]: ./media/best-practices-network-security/example4networklogical.png "NVA 관점에서의 논리적 네트워크"
[14]: ./media/best-practices-network-security/example5designoptions.png "사이트 간 하이브리드 네트워크를 통해 Azure 게이트웨이에 연결된 DMZ"
[15]: ./media/best-practices-network-security/example5designs2s.png "사이트 간 VPN을 사용하는 Azure 게이트웨이가 있는 DMZ"
[16]: ./media/best-practices-network-security/example6designoptions.png "Azure 게이트웨이 연결 Express 경로 하이브리드 네트워크가 있는 DMZ"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Express 경로 연결을 사용하는 Azure 게이트웨이가 있는 DMZ"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md

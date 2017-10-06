---
title: "Azure 응용 프로그램 게이트웨이에 대 한 질문과 대답 aaaFrequently | Microsoft Docs"
description: "이 페이지에서는 답변 toofrequently Azure 응용 프로그램 게이트웨이에 대 한 질문과 대답"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Application Gateway에 대한 질문과 대답

## <a name="general"></a>일반

**Q. Application Gateway란?**

Azure Application Gateway는 서비스 형태의 ADC(응용 프로그램 전달 컨트롤러)이며 응용 프로그램에 대한 다양한 계층 7 부하 분산 기능을 제공합니다. Azure에서 완전히 관리되는 고가용성의 확장성 있는 서비스를 제공합니다.

**Q. Application Gateway에서 지원하는 기능은 어떤 것이 있나요?**

응용 프로그램 게이트웨이 SSL 오프 로딩 및 끝 tooend SSL, 웹 응용 프로그램 방화벽, 쿠키 기반 세션 선호도, url 경로 기반 라우팅, 다중 사이트 호스팅 및 다른 사용자를 지원 합니다. 지원 되는 기능의 전체 목록을 보려면 방문 [소개 tooApplication 게이트웨이](application-gateway-introduction.md)

**Q. 응용 프로그램 게이트웨이와 Azure 부하 분산 장치 간의 hello 차이점은 무엇입니까?**

Application Gateway는 웹 트래픽(HTTP/HTTPS/WebSocket)에서만 작동하는 7계층 부하 분산 장치로서 합니다. SSL 종료, 쿠키 기반 세션 선호도, 트래픽 부하 분산을 위한 라운드 로빈과 같은 기능을 지원합니다. 부하 분산 장치, 계층 4(TCP/UDP)에서 트래픽 부하 분산.

**Q. Application Gateway에서 지원하는 프로토콜은 무엇인가요?**

Application Gateway는 HTTP, HTTPS 및 WebSocket을 지원합니다.

**Q. 현재 백 엔드 풀의 일부로 어떤 리소스가 지원되나요?**

백 엔드 풀은 NIC, 가상 컴퓨터 확장 집합, 공용 IP, 내부 IP, FQDN(정규화된 도메인 이름) 및 다중 테넌트 백 엔드(예: Azure Web Apps)로 구성될 수 있습니다. 응용 프로그램 게이트웨이 백 엔드 풀 멤버가 하지 않습니다. tooan 가용성 집합을 연결 합니다. 백 엔드 풀의 멤버는 IP 연결이 있는 경우 클러스터, 데이터 센터 간 또는 Azure 외부에 있을 수 있습니다.

**Q. 어떤 영역은 hello 서비스에서 사용할 수 있습니까?**

Application Gateway는 Azure 전체의 모든 지역에서 사용할 수 있습니다. [Azure China](https://www.azure.cn/) 및 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)에서도 사용할 수 있습니다.

**Q. 내 구독에 대한 전용 배포인가요? 아니면 고객 간에 공유되나요?**

Application Gateway는 가상 네트워크에서 전용 배포입니다.

**Q. HTTP->HTTPS 리디렉션이 지원되나요?**

리디렉션은 지원됩니다. 방문 [응용 프로그램 게이트웨이 리디렉션 개요](application-gateway-redirect-overview.md) toolearn 더 합니다.

**Q. 수신기는 어떤 순서로 처리되나요?**

수신기는 표시 된 hello 순서 대로 처리 됩니다. 이러한 이유로 기본 수신기에서 들어오는 요청과 일치하는 경우 이 요청을 먼저 처리합니다.  다중 사이트 수신기 기본 수신기 tooensure 트래픽 라우팅된 toohello 올바른 백 엔드 되기 전에 구성 되어야 합니다.

**Q. Application Gateway의 IP 및 DNS는 어디에서 확인하나요?**

공용 IP 주소를 끝점으로 사용할 경우이 정보가 있습니다 hello 개요 페이지에서 또는 hello 공용 IP 주소 리소스에 hello 포털에서 응용 프로그램 게이트웨이 hello에 대 한 합니다. 내부 IP 주소에 대 한 hello 개요 페이지에서 찾을 수 있습니다.

**Q. 가 hello IP 또는 DNS 변경 hello 응용 프로그램 게이트웨이 hello 기간 동안 합니까?**

hello VIP hello 게이트웨이 중지 되 고 hello 고객에서 시작 하는 경우 변경할 수 있습니다. 응용 프로그램 게이트웨이에 연결 된 DNS hello hello 게이트웨이의 hello 수명 주기를 통해 변경 되지 않습니다. 이러한 이유로 toouse CNAME 별칭을 권장 하 고 응용 프로그램 게이트웨이 hello toohello DNS 주소를 가리킵니다.

**Q. Application Gateway에서 고정 IP를 지원하나요?**

아니요, Application Gateway에서는 고정 공용 IP 주소를 지원하지 않고 고정 내부 IP를 지원합니다.

**Q. 응용 프로그램 게이트웨이 hello 게이트웨이에 여러 공용 Ip를 지원 합니까?**

Application Gateway에서는 하나의 공용 IP 주소만 지원됩니다.

**Q. Application Gateway에서 x-forwarded-for 헤더를 지원하나요?**

예, x-전달-프로토콜, x-전달 기능에 대 한 응용 프로그램 게이트웨이 삽입 하 고 hello 요청으로 x 전달 포트 헤더가 toohello 백 엔드 전달. x-전달 기능에 대 한 헤더에 대 한 hello 형식은 쉼표로 구분 된 목록 ip: port입니다. hello x 전달 프로토콜에 대 한 유효한 값은 http 또는 https입니다. X 전달 된 포트에 응용 프로그램 게이트웨이 hello에 도달 하는 hello 요청 시 hello 포트를 지정 합니다.

**Q. 얼마나 오래 걸립니까 toodeploy 응용 프로그램 게이트웨이? Application Gateway가 업데이트되어도 여전히 작동하나요?**

새 응용 프로그램 게이트웨이 배포 too20 분 tooprovision 차지할 수 있습니다. 변경 내용을 tooinstance 크기/수 장치를 중단할 필요가 되지 않으며 hello 게이트웨이이 시간 동안 활성 상태로 유지 합니다.

## <a name="configuration"></a>구성

**Q. Application Gateway가 가상 네트워크에서 항상 배포되나요?**

예, Application Gateway는 항상 가상 네트워크 서브넷에 배포됩니다. 이 서브넷은 Application Gateway만 포함할 수 있습니다.

**Q. 응용 프로그램 게이트웨이 해당 가상 네트워크 외부 tooinstances 서로 연결할 수 있습니까?**

응용 프로그램 게이트웨이 IP로 연결 되어으로 컴퓨터가 hello 가상 네트워크 외부에서 tooinstances를 문의 수 있습니다. 백 엔드 풀 멤버 이면 내부 Ip 필요 toouse 계획 이라면 [VNET 피어 링](../virtual-network/virtual-network-peering-overview.md) 또는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.

**Q. 배포할 수 있습니까 hello 응용 프로그램 게이트웨이 서브넷의 다른 부분?**

아니요, 하지만 hello 서브넷에서 다른 응용 프로그램 게이트웨이 배포할 수 있습니다.

**Q. Hello 응용 프로그램 게이트웨이 서브넷에 네트워크 보안 그룹 지원 되나요?**

네트워크 보안 그룹은 다음 제한 사항이 hello로 hello 응용 프로그램 게이트웨이 서브넷에서 지원 됩니다.

* 예외에 배치 해야 들어오는 트래픽에 대 한 백 엔드 상태 toowork에 대 한 65503 65534 포트에서 올바르게 합니다.

* 아웃바운드 인터넷 연결은 차단할 수 없습니다.

* Hello AzureLoadBalancer 태그에서에서 트래픽을 허용 되어야 합니다.

**Q. 응용 프로그램 게이트웨이 hello 제한 사항은 무엇입니까? 이러한 한도를 늘릴 수 있나요?**

방문 [응용 프로그램 게이트웨이 제한](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello 제한 합니다.

**Q. 외부 및 내부 트래픽 모두에 Application Gateway를 동시에 사용할 수 있나요?**

예, Application Gateway에서는 Application Gateway당 내부 IP 하나와 외부 IP 하나를 지원합니다.

**Q. VNet 피어링이 지원되나요?**

예, VNet 피어링이 지원되며 다른 가상 네트워크에서 트래픽을 부하 분산시키는 데 도움이 됩니다.

**Q. 문의 해야 합니까 tooon 온-프레미스 서버 ExpressRoute 또는 VPN 터널으로 연결 되어 있습니까?**

예, 트래픽이 허용되기만 한다면 가능합니다.

**Q. 한 개의 백 엔드 풀에서 서로 다른 포트로 많은 응용 프로그램을 제공할 수 있나요?**

마이크로 서비스 아키텍처가 지원됩니다. 서로 다른 포트에서 여러 http 구성 된 설정을 tooprobe를 해야 합니다.

**Q. 사용자 지정 프로브가 응답 데이터에 와일드 카드/regex를 지원하나요?**

사용자 지정 프로브는 응답 데이터에 와일드 카드 또는 regex를 지원하지 않습니다. 

**Q. 규칙은 어떻게 처리되나요?**

규칙은 구성 된 hello 순서로 처리 됩니다. Hello 기본 규칙 평가 되는 포트 이전 toohello 다중 사이트 규칙에 따라 트래픽의 일치 하는 기본 규칙 tooreduce hello 가능성이 트래픽이 toohello 부적절 한 백 엔드를 라우트하기 전에 멀티 사이트 규칙이 구성 된 것이 좋습니다.

**Q. 규칙은 어떻게 처리되나요?**

규칙은 만들어질 hello 순서로 처리 됩니다. 다중 사이트 규칙이 기본 규칙보다 먼저 구성되는 것이 좋습니다. 다중 사이트 수신기를 먼저 구성 하면이 구성은 트래픽이 라우트된 toohello 부적절 한 백 엔드 되 hello 가능성을 줄입니다. Hello 기본 규칙 평가 되는 포트 이전 toohello 다중 사이트 규칙에 따라 트래픽의 일치 하는 것이 라우팅 문제가 발생할 수 있습니다.

**Q. 사용자 지정 프로브에 대해 hello 호스트 필드는 나타낼 하는?**

호스트 필드는 hello 이름 toosend hello 검색을 실행 하려면를 지정합니다. 다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다. 이 값은 VM 호스트 이름과 다르며 \<프로토콜\>://\<호스트\>:\<포트\>\<경로\> 형식입니다.

**Q. 수 있는 응용 프로그램 게이트웨이 액세스 tooa 화이트 리스트 Ip 소스 지원 되는 몇?**

이 시나리오는 Application Gateway 서브넷에서 NSG를 사용하여 수행할 수 있습니다. 우선 순위에 따라 나열 된 hello hello 서브넷에 넣을 hello 다음 제한 사항:

* 원본 IP/IP 범위에서 들어오는 트래픽을 허용합니다.

* 들어오는 요청에 대 한 모든 소스 tooports 65503 65534 허용 [백 엔드 상태 통신](application-gateway-diagnostics.md)합니다.

* Hello에 대 한 들어오는 Azure 부하 분산 장치 프로브 (AzureLoadBalancer 태그)와 가상 인바운드 네트워크 트래픽을 (VirtualNetwork 태그) 가능 [NSG](../virtual-network/virtual-networks-nsg.md)합니다.

* 모두 거부 규칙을 사용하여 다른 모든 들어오는 트래픽을 차단합니다.

* 아웃 바운드 트래픽을 toohello 허용 모든 대상에 대 한 인터넷 합니다.

## <a name="performance"></a>성능

**Q. Application Gateway는 고가용성과 확장성을 어떤 방식으로 지원하나요?**

둘 이상의 인스턴스가 배포된 경우에 Application Gateway에서 고가용성 시나리오를 지원합니다. Azure hello에서 모든 인스턴스가 실패 하지 않는 업데이트 및 오류 도메인 tooensure 분산 이러한 인스턴스에 동일한 시간입니다. 응용 프로그램 게이트웨이 hello의 여러 인스턴스를 추가 하 여 확장성을 지원 게이트웨이 tooshare hello 부하를 동일 합니다.

**Q. Application Gateway에서 데이터 센터 간 DR 시나리오를 어떻게 달성할 수 있나요?**

고객이 다른 데이터 센터에서 여러 응용 프로그램 게이트웨이 트래픽 관리자 toodistribute 트래픽을 사용할 수 있습니다.

**Q. 자동 크기 조정이 지원되나요?**

아니요, 하지만 응용 프로그램 게이트웨이 처리량 메트릭을 사용 하는 tooalert 일 수 있는 하 한 임계값에 도달 합니다. 수동으로 인스턴스를 추가 또는 크기를 변경 hello 게이트웨이 다시 시작 되지 않으면 하며 기존 트래픽을 영향을 주지 않습니다.

**Q. 수동 강화/규모 축소 시 가동 중지 시간이 발생하나요?**

가동 중지 시간 없이 인스턴스가 업그레이드 도메인 및 장애 도메인 간에 배포됩니다.

**Q. 중지 하지 않고 중간 toolarge 인스턴스 크기를 변경할 수 있나요?**

Azure hello에서 모든 인스턴스가 실패 하지 않는 업데이트 및 오류 도메인 tooensure에서 인스턴스를 배포 하는 예, 같은 시간입니다. 여러 인스턴스를 추가 하 여 크기 조정 응용 프로그램 게이트웨이 지원 hello 게이트웨이 tooshare hello 부하를 동일 합니다.

## <a name="ssl-configuration"></a>SSL 구성

**Q. Application Gateway에서 어떤 인증서가 지원되나요?**

자체 서명된 인증서, CA 인증서 및 와일드 카드 인증서가 지원됩니다. EV 인증서는 지원되지 않습니다.

**Q. 응용 프로그램 게이트웨이 원하는 hello 현재 암호 그룹은 무엇입니까?**

hello 다음 원하는 응용 프로그램 게이트웨이 hello 현재 암호 그룹은입니다. 방문: [SSL 구성 정책 버전 및 응용 프로그램 게이트웨이에 암호 그룹](application-gateway-configure-ssl-policy-powershell.md) toolearn 어떻게 toocustomize SSL 옵션입니다.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**Q. 트래픽 toohello 백 엔드를 다시 암호화는 응용 프로그램 게이트웨이도 지원 합니까?**

예, 응용 프로그램 게이트웨이 지원 SSL 오프 로드 및 끝 tooend hello 트래픽 toohello 백 엔드를 다시 암호화 하는 SSL 합니다.

**Q. SSL 정책 toocontrol SSL 프로토콜 버전을 구성할 수 있습니까?**

예, 응용 프로그램 게이트웨이 toodeny를 구성할 수 있습니다 TLS1.0, TLS1.1 및 TLS1.2 합니다. SSL 2.0 및 3.0은 기본적으로 비활성화되며 구성할 수 없습니다.

**Q. 암호 그룹 및 정책 순서를 구성할 수 있나요?**

예, [암호 그룹을 구성](application-gateway-ssl-policy-overview.md)하도록 지원됩니다. 사용자 지정 정책의 정의할 때는 hello 암호 그룹이 다음 중 하나 이상이 사용 되어야 합니다. 응용 프로그램 게이트웨이 s h a 256 toofor 백 엔드 관리를 사용합니다.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**Q. 몇 개의 SSL 인증서가 지원되나요?**

too20 SSL 인증서 지원 됩니다.

**Q. 백 엔드 재암호화에 몇 개의 인증 인증서가 지원되나요?**

Too10를 인증 인증서는 이며 기본값은 5 지원 됩니다.

**Q. Application Gateway가 Azure Key Vault와 고유하게 통합되나요?**

아니요, Azure Key Vault와 통합되지 않습니다.

## <a name="web-application-firewall-waf-configuration"></a>WAF(웹 응용 프로그램 방화벽) 구성

**Q. Hello WAF SKU hello 표준 SKU로 사용할 수 있는 모든 hello 기능을 제공 합니까?**

예, WAF hello 표준 SKU의에서 모든 hello 기능을 지원합니다.

**Q. 응용 프로그램 게이트웨이 지원 hello CRS 버전은 무엇입니까?**

Application Gateway는 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 및 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)을 지원합니다.

**Q. WAF를 모니터링하려면 어떻게 하나요?**

WAF는 진단 로깅을 통해 모니터링되며 진단 로깅에 대한 자세한 내용은 [Application Gateway에 대한 진단 로깅 및 메트릭](application-gateway-diagnostics.md)에서 확인할 수 있습니다.

**Q. 검색 모드에서 트래픽을 차단하나요?**

아니요, 검색 모드는 WAF 규칙을 트리거한 트래픽만 로깅합니다.

**Q. WAF 규칙을 사용자 지정하려면 어떻게 하나요?**

예, WAF 규칙은 toocustomize을 방문할 방법에 대 한 자세한 내용은 사용자 지정 가능한 [WAF 사용자 지정 규칙 그룹 및 규칙](application-gateway-customize-waf-rules-portal.md)

**Q. 현재 사용 가능한 규칙은 무엇인가요?**

WAF CRS는 현재 지원 [2.2.9 퀵](application-gateway-crs-rulegroups-rules.md#owasp229) 및 [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), 대부분의 hello에 대 한 초기 보안을 제공 하는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) ´ ֿ ´로 식별 되는 상위 10 개의 취약성 [OWASP 상위 10 개의 취약성](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* SQL 삽입 공격 보호

* 교차 사이트 스크립팅 공격 보호

* 명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호

* HTTP 프로토콜 위반 보호

* 누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호

* 보트, 크롤러 및 스캐너 방지

* 일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색

**Q. WAF에서 DDoS 방지도 지원하나요?**

아니요, WAF는 DDoS 방지를 제공하지 않습니다.

## <a name="diagnostics-and-logging"></a>진단 및 로깅

**Q. Application Gateway에서 어떤 유형의 로그를 사용할 수 있나요?**

Application Gateway에서는 3가지 로그를 사용할 수 있습니다. 이러한 로그 및 기타 진단 기능에 대한 자세한 내용은 [Application Gateway에 대한 백 엔드 상태, 진단 로깅 및 메트릭](application-gateway-diagnostics.md)을 참조하세요.

- **ApplicationGatewayAccessLog** -hello 액세스 로그에 제출 된 각 요청 toohello 응용 프로그램 게이트웨이 프런트 엔드 합니다. 축소 및 반환 코드, 바이트, hello 데이터 hello 호출자의 IP, URL, 요청 응답 대기 시간이 포함 됩니다. 액세스 로그는 300초마다 수집됩니다. 이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다.
- **ApplicationGatewayPerformanceLog** -hello 성능 로그에 정보가 성능 인스턴스별로 서비스를 제공 하는 총 요청을 포함 하 여 처리량 (바이트), 총 요청 제공을 정상 및 비정상 실패 한 요청 수 백 엔드 인스턴스 수입니다.
- **ApplicationGatewayFirewallLog** -hello 방화벽 로그 감지 하거나 방지 모드의 웹 응용 프로그램 방화벽으로 구성 된 응용 프로그램 게이트웨이 통해 기록 된 요청을 포함 합니다.

**Q. 내 백 엔드 풀 멤버가 정상인지 어떻게 알 수 있나요?**

Hello PowerShell cmdlet을 사용할 수 있습니다 `Get-AzureRmApplicationGatewayBackendHealth` 방문 하 여 hello 포털을 통해 상태를 확인 또는 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)

**Q. Hello 진단 로그에 hello 보존 정책 이란?**

진단 로그 흐름 toohello 고객 저장소 계정 및 고객의 기본 설정에 따라 hello 보존 정책을 설정할 수 있습니다. 진단 로그 이벤트 허브 또는 로그 분석 tooan을 보낼 수도 있습니다. 자세한 내용을 보려면 [Application Gateway 진단](application-gateway-diagnostics.md)을 방문하세요.

**Q. Application Gateway에 대한 감사 로그를 어떻게 얻나요?**

Application Gateway에 대해 감사 로그를 사용할 수 있습니다. Hello 포털에서 클릭 **활동 로그** 응용 프로그램 게이트웨이 tooaccess hello 감사 로그의 hello 메뉴 블레이드에서 합니다. 

**Q. Application Gateway로 경고를 설정할 수 있나요?**

예, Application Gateway는 경고를 지원하며 메트릭에 따라 경고를 해제하도록 구성합니다.  현재 응용 프로그램 게이트웨이 보유 한 메트릭 "처리량" tooalert 구성된 될 수 있습니다. 경고에 대 한 더 toolearn 방문 [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.

**Q. 백 엔드 상태에서 알 수 없는 상태를 반환할 경우 이 상태의 원인은 무엇인가요?**

hello 가장 일반적인 이유는 액세스 toohello 백 엔드는 NSG 나 사용자 지정 DNS에서 차단 되 고 있습니다. 방문 [백 엔드 상태, 진단 로깅 및 응용 프로그램 게이트웨이 대 한 메트릭을](application-gateway-diagnostics.md) toolearn 더 합니다.

## <a name="next-steps"></a>다음 단계

응용 프로그램 게이트웨이에 대해 자세히 방문 toolearn [소개 tooApplication 게이트웨이](application-gateway-introduction.md)합니다.

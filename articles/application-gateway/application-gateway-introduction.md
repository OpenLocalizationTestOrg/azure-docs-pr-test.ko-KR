---
title: "응용 프로그램 게이트웨이 aaaIntroduction tooAzure | Microsoft Docs"
description: "이 페이지 계층 7 부하 분산에 대 한 hello 응용 프로그램 게이트웨이 서비스에 대해 간략하게 게이트웨이 크기를 포함 하 여, HTTP 부하 분산, 쿠키 기반 세션 선호도 및 제공 SSL 오프 로드 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Application Gateway에 대한 개요

Microsoft Azure Application Gateway는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하는 전용 가상 어플라이언스입니다. 응용 프로그램에 다양한 레이어 7 부하 분산 기능을 제공합니다. 이 통해 고객 toooptimize 웹 팜 생산성 CPU 집약적인 SSL 종료 toohello 응용 프로그램 게이트웨이 오프 로드 합니다. 들어오는 트래픽을, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅 및 hello 기능 toohost 라운드 로빈 배포를 포함 하는 다른 계층 7 라우팅 기능 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트도 제공 합니다. 웹 응용 프로그램 방화벽 (WAF) hello 응용 프로그램 게이트웨이 WAF SKU의 일부로 제공 됩니다. 일반적인 웹 취약점을 악용 tooweb 응용 프로그램 보호 제공합니다. Application Gateway는 인터넷 연결 게이트웨이, 내부 전용 게이트웨이 또는 둘의 조합으로 구성할 수 있습니다. 

![시나리오](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>기능

현재 응용 프로그램 게이트웨이 기능을 수행 하는 hello를 제공 합니다.


* **[웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)**  -hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호 합니다.
* **HTTP 부하 분산** - Application Gateway는 라운드 로빈 부하 분산을 제공합니다. 부하 분산은 계층 7에서 수행되고 HTTP(S) 트래픽에 대해서만 사용됩니다.
* **쿠키 기반 세션 선호도** -tookeep hello에 사용자 세션을 원하는 경우 쿠키 기반 세션 선호도 기능 hello 유용 합니다. 동일한 백 엔드 합니다. 게이트웨이 관리 쿠키를 사용 하 여 hello 응용 프로그램 게이트웨이 사용자 세션 toohello에서 수 toodirect 후속 트래픽 처리를 위해 동일한 백 엔드 합니다. 이 기능은 세션 상태가 저장 되 로컬로 hello 백 엔드 서버에서 사용자 세션에 대 한 경우에 특히 중요 합니다.
* **[Secure Sockets Layer (SSL) 오프 로드](application-gateway-ssl-arm.md)**  -이 기능은 HTTPS 트래픽을 웹 서버를 암호 해독 hello 비용이 많이 드는 작업을 사용 합니다. 종결 hello hello 응용 프로그램 게이트웨이 및 전달 암호화 되지 않은 hello 요청 toohello 서버에서 SSL 연결을 여 hello 웹 서버는 암호 해독 하 여 unburdened 됩니다.  응용 프로그램 게이트웨이 백 toohello 클라이언트를 보내기 전에 hello 응답을 다시 암호화 합니다. 이 기능은 hello 백 엔드 인 시나리오에서 유용 hello에 동일한 가상 네트워크 보안을 유지 하 Azure에서 응용 프로그램 게이트웨이 hello 합니다.
* **[TooEnd SSL 종료](application-gateway-backend-ssl.md)**  -응용 프로그램 게이트웨이 지원 종료 트래픽의 tooend 암호화 합니다. 응용 프로그램 게이트웨이 hello 응용 프로그램 게이트웨이에서 hello SSL 연결을 종료 하 여이 작업을 수행 합니다. hello 게이트웨이 toohello 트래픽을 다시 hello 패킷 암호화 및 hello 패킷 toohello 적절 한 백 엔드 hello 라우팅 규칙 정의에 따라 전달 hello 라우팅 규칙을 적용 합니다. Hello 웹 서버에서 받은 모든 응답 hello를 통해 이동 백 toohello 최종 사용자를 처리 하는 동일 합니다.
* **[콘텐츠 라우팅 URL 기반](application-gateway-url-route-overview.md)**  -이 기능을 통해 hello 기능 toouse 다른 백 엔드 서버에 각 트래픽입니다. CDN 또는 hello 웹 서버에 있는 폴더에 대 한 트래픽 라우팅된 tooa 다른 백 엔드 될 수 있습니다. 이 기능은 특정 콘텐츠에 서비스를 제공하지 않는 백 엔드에 대한 불필요한 부하를 줄입니다.
* **[다중 사이트 라우팅](application-gateway-multi-site-overview.md)**  -응용 프로그램 게이트웨이 tooconsolidate too20 단일 응용 프로그램 게이트웨이 웹 사이트를 허용 합니다.
* **[Websocket 지원](application-gateway-websocket.md)**  -응용 프로그램 게이트웨이의 또 다른 유용한 기능은 hello 기본적으로 지원 되는 Websocket 됩니다.
* **[상태 모니터링](application-gateway-probe-overview.md)**  -응용 프로그램 게이트웨이 백 엔드 리소스의 모니터링 및 사용자 지정의 기본 상태 프로브 toomonitor 보다 구체적인 시나리오를 제공 합니다.
* **[SSL 정책 및 암호화](application-gateway-ssl-policy-overview.md)**  -이 기능은 toolimit hello SSL 프로토콜 버전 hello 기능을 제공 하 고 hello 암호 제품군에는 처리 순서 hello 및 지원 됩니다.
* **[리디렉션 요청](application-gateway-redirect-overview.md)**  -이 기능 hello 기능 tooredirect HTTP 요청 tooan HTTPS 수신기를 제공 합니다.
* **[다중 테넌트 백 엔드 지원](application-gateway-web-app-overview.md)**  - 응용 프로그램 게이트웨이는 Azure Web Apps 및 API Gateway 같은 다중 테넌트 백 엔드 서비스를 백 엔드 풀 멤버로 구성하는 기능을 지원합니다. 
* **[고급 진단](application-gateway-diagnostics.md)** - Application Gateway는 전체 진단 및 액세스 로그를 제공합니다. 방화벽 로그는 WAF를 사용할 수 있는 Application Gateway 리소스에 사용할 수 있습니다.

## <a name="benefits"></a>이점

Application Gateway는 다음과 같은 경우에 유용합니다.

* 응용 프로그램 요청 해야 하는 hello에서 동일한 사용자/클라이언트 세션 tooreach hello 동일한 백 엔드 가상 컴퓨터. 이러한 응용 프로그램의 예로는 쇼핑 카트 응용 프로그램 및 웹 메일 서버가 있습니다.
* 웹 서버 팜에 대한 SSL 종료 오버 헤드를 제거합니다.
* Hello 같은 장기 실행 TCP 연결 toobe 라우팅되거나 로드 균형 잡힌된 toodifferent 백 엔드 서버에서 여러 HTTP 요청 해야 하는 콘텐츠 배달 네트워크 등의 응용 프로그램입니다.
* websocket 트래픽을 지원하는 응용 프로그램
* SQL 삽입, 사이트 간 스크립팅 공격, 세션 하이재킹과 같은 일반적인 웹 기반 공격으로부터 웹 응용 프로그램을 보호합니다.
* 논리적인 트래픽 분배는 URL 경로 또는 도메인 헤더와 같은 다른 라우팅을 기반으로 합니다.

Application Gateway는 전적으로 Azure에 의해 관리되고, 확장성 및 고가용성을 제공합니다. 관리 효율성을 향상시키기 위한 풍부한 진단 및 로깅 기능을 제공합니다. 응용 프로그램 게이트웨이를 만들 때 끝점(공용 VIP 또는 내부 ILB IP)이 연결되어 수신 네트워크 트래픽에 사용됩니다. 이 VIP 또는 ILB IP (TCP/UDP) hello 전송 수준에서 작동 하 고 들어오는 모든 네트워크 트래픽 부하 분산 된 toohello 응용 프로그램 게이트웨이 작업자 인스턴스 되 고 Azure 부하 분산 장치에서 제공 됩니다. 경로 가상 컴퓨터 인지 해당 구성에 따라 HTTP/HTTPS 트래픽을 hello 다음 응용 프로그램 게이트웨이 hello 클라우드 서비스, 내부 또는 외부 IP 주소입니다.

응용 프로그램 게이트웨이 부하 분산 하는 Azure에서 관리 하는 서비스 내에 허용 hello hello Azure 소프트웨어 부하 분산 장치 뒤 layer 7 부하 분산 장치 프로 비전 합니다. 다음 이미지, 트래픽 관리자를 제공 하는 리디렉션 및 트래픽의 가용성을 다른 지역에 toomultiple 응용 프로그램 게이트웨이 리소스 응용 프로그램 게이트웨이 제공 하는 동안 hello와 같이 트래픽 관리자 사용된 toocomplete hello 시나리오 수 있습니다. 영역 계층 7 부하 분산을 교차 합니다. 이 시나리오의 예제에서 확인할 수 있습니다: [를 사용 하 여 부하 분산에 hello Azure 클라우드 서비스](../traffic-manager/traffic-manager-load-balancing-azure.md)

![Traffic Manager 및 Application Gateway 시나리오](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>게이트웨이 크기 및 인스턴스

Application Gateway는 현재 **소형**, **중형** 및 **대형**의 3가지 크기를 제공합니다. 소규모 인스턴스 크기는 개발 및 테스트 시나리오를 위해 사용 됩니다.

구독 당 too50 응용 프로그램 게이트웨이를 만들 수 있습니다 및 각 응용 프로그램 게이트웨이 too10 인스턴스를 만들 수 있습니다. 각 Application Gateway는 http 수신기 20개로 구성할 수 있습니다. Application Gateway의 전체 목록은 [Application Gateway 서비스 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits)을 참조하세요.

다음 표에서 hello SSL 오프 로드를 사용 하도록 설정 된 각 응용 프로그램 게이트웨이 인스턴스는 평균 성능 처리량을 보여 줍니다.

| 백 엔드 페이지 응답 | 작음 | 중간 | 큼 |
| --- | --- | --- | --- |
| 6K |7.5Mbps |13Mbps |50Mbps |
| 100K |35Mbps |100Mbps |200Mbps |

> [!NOTE]
> 이러한 값은 응용 프로그램 게이트웨이 처리량에 대한 대략적인 값입니다. hello 실제 처리량에 따라 달라 집니다 평균 페이지 크기를 비롯 한 다양 한 환경 세부 백 엔드 인스턴스 및 처리 시간 tooserve 페이지의 위치입니다. 정확한 성능 수치를 얻으려면 자체 테스트를 실행해야 합니다. 이러한 값은 용량 계획 지침에 대해서만 제공됩니다.

## <a name="health-monitoring"></a>상태 모니터링

Azure 응용 프로그램 게이트웨이 자동으로 기본 또는 사용자 정의 상태 프로브를 통해 백 엔드 인스턴스 hello hello 상태를 모니터링합니다. 상태 프로브를 사용 하 여 정상만 호스트 응답 tootraffic 있는지 확인 합니다. 자세한 내용은 [Application Gateway 상태 모니터링 개요](application-gateway-probe-overview.md)를 참조하세요.

## <a name="configuring-and-managing"></a>구성 및 관리

Azure Application Gateway는 구성된 경우 끝점으로 공용 IP, 개인 IP 또는 둘 다를 가질 수 있습니다. Application Gateway는 고유한 서브넷의 가상 네트워크 내에서 구성됩니다. hello 서브넷 만들거나 응용 프로그램 게이트웨이를 사용 하는 다른 유형의 리소스를 포함할 수 없습니다, 그리고 hello 리소스가 hello 서브넷에서 허용 하는 다른 응용 프로그램 게이트웨이 합니다. toosecure hello에서 다른 서브넷 내에서 백엔드 리소스, hello 백 엔드 서버를 포함 될 수 있는 응용 프로그램 게이트웨이 hello와 동일한 가상 네트워크입니다. 이 서브넷이 hello 백 엔드 응용 프로그램에 대 한 필요 하지 않습니다. Hello 응용 프로그램 게이트웨이 hello ip 주소에 연결할 수으로 응용 프로그램 게이트웨이 백 엔드 서버 hello에 대 한 수 tooprovide ADC 기능입니다. 

REST API, PowerShell cmdlets, Azure CLI 또는 [Azure Portal](https://portal.azure.com/)을 사용하여 Application Gateway를 만들고 관리할 수 있습니다. 응용 프로그램 게이트웨이 추가 질문이 있으면 방문 [응용 프로그램 게이트웨이 FAQ](application-gateway-faq.md) tooview 공통의 목록에 대 한 질문과 대답입니다.

## <a name="pricing"></a>가격

가격 책정은 시간 당 게이트웨이 인스턴스 요금 및 데이터 처리 충전을 기반으로 합니다. 시간당 hello WAF SKU에 대 한 가격 책정 게이트웨이 표준 SKU 요금와에서 다릅니다. 이 요금 정보는 [Application Gateway 가격 책정 정보](https://azure.microsoft.com/pricing/details/application-gateway/)에서 확인할 수 있습니다. 데이터 처리 요금이 계속 hello 동일 합니다.

## <a name="faq"></a>FAQ

Application Gateway에 대한 자주 묻는 질문은 [Application Gateway FAQ](application-gateway-faq.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

수 응용 프로그램 게이트웨이에 대 한 학습 한 후 [응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md) 할 수도 있습니다 [SSL 오프 로드 하는 응용 프로그램 게이트웨이 만들기](application-gateway-ssl-arm.md) tooload 분산 HTTPS 연결 합니다.

toolearn 어떻게 toocreate 콘텐츠 라우팅 URL 기반을 사용 하 여 응용 프로그램 게이트웨이 이동 너무[URL 기반 라우팅을 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-url-route-arm-ps.md) 자세한 정보에 대 한 합니다.

toolearn 중 일부에 대 한 다른 키를 Azure의 기능 네트워킹 hello를 참조 하십시오. [Azure 네트워킹](../networking/networking-overview.md)합니다.

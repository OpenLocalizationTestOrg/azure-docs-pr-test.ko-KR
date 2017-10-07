---
title: "aaaWhat은 트래픽 관리자 | Microsoft Docs"
description: "이 문서가 트래픽 관리자는 기능 및 응용 프로그램에 대 한 hello 오른쪽 트래픽 라우팅 항목 인지를 이해 하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Traffic Manager 개요

Microsoft Azure 트래픽 관리자 다른 데이터 센터에서 서비스 끝점에 대 한 사용자 트래픽의 toocontrol hello 배포를 사용 합니다. Traffic Manager에서 지원되는 서비스 끝점은 Azure VM, Web Apps 및 클라우드 서비스를 포함합니다. 또한 외부, Azure가 아닌 끝점으로 Traffic Manager를 사용할 수 있습니다.

트래픽 관리자 끝점을 사용 하 hello DNS 도메인 이름 () toodirect 클라이언트 요청 toohello 가장 적합 한 hello 끝점의 hello 상태와는 트래픽 라우팅 방법에 따라 합니다. 트래픽 관리자는 다양 한 제공 [트래픽 라우팅 방법](traffic-manager-routing-methods.md) 및 [끝점 모니터링 옵션](traffic-manager-monitoring.md) toosuit 다른 응용 프로그램 요구 사항 및 자동 장애 조치 모델. 트래픽 관리자는 전체 Azure 지역의 hello 못하고 탄력적 toofailure입니다.

## <a name="traffic-manager-benefits"></a>Traffic Manager 이점

Traffic Manager은 다음과 같은 작업에 도움이 될 수 있습니다.

* **중요 응용 프로그램의 가용성 향상**

    Traffic Manager는 끝점을 모니터링하여 끝점이 중단될 경우 자동 장애 조치를 제공함으로써 응용 프로그램에 대한 높은 가용성을 제공합니다.

* **고성능 응용 프로그램의 응답성 향상**

    Azure가 있습니다 toorun 클라우드 서비스나 웹 사이트 hello 전 세계에 있는 데이터 센터에서. 트래픽 관리자 hello 가장 낮은 hello 클라이언트에 대 한 네트워크 대기 시간으로 트래픽 toohello 끝점을 연결 하 여 응용 프로그램의 응답성을 향상 시킵니다.

* **가동 중지 시간 없이 서비스 유지 관리 수행**

    가동 중지 시간 없이 응용 프로그램에 계획된 유지 관리 작업을 수행할 수 있습니다. 트래픽 관리자는 hello 유지 관리 진행 중인 동안 트래픽이 tooalternative 끝점을 전달 합니다.

* **온-프레미스와 클라우드 기반 응용 프로그램의 결합**

    트래픽 관리자 외부, 지원 toobe 하이브리드 함께 사용 하도록 설정 하는 비 Azure 끝점 클라우드 및 온-프레미스 배포 hello "버스트-클라우드," "마이그레이션-클라우드," 및 "장애 조치 클라우드" 시나리오입니다.

* **복잡한 대규모 배포를 위한 트래픽 분산**

    사용 하 여 [트래픽 관리자 프로필을 중첩](traffic-manager-nested-profiles.md), 트래픽 라우팅 방법이 결합된 toocreate 정교한 될 수 있습니다 및 유연한 규칙 toosupport hello 큰, 보다 복잡 한 배포의 필요성을 해결 합니다.

## <a name="how-traffic-manager-works"></a>트래픽 관리자 작동 방식

Azure 트래픽 관리자 응용 프로그램 끝점에서 트래픽의 toocontrol hello 배포를 사용합니다. 끝점은 Azure의 내부 또는 외부에서 호스팅되는 모든 인터넷 연결 서비스입니다.

Traffic Manager는 다음과 같은 두 가지 주요 이점을 제공합니다.

1. 일부의 tooone에 따라 트래픽의 배포 [트래픽 라우팅 메서드](traffic-manager-routing-methods.md)
2. [끝점 상태 연속 모니터링](traffic-manager-monitoring.md) 및 끝점이 실패할 경우 자동 장애 조치(failover)

클라이언트가 tooconnect tooa 서비스 때 hello 서비스 tooan IP 주소의 DNS 이름을 hello를 먼저 해결 해야 합니다 것입니다. 클라이언트 hello toothat IP 주소 tooaccess hello 서비스를 연결합니다.

**가장 중요 한 지점을 toounderstand hello 트래픽 관리자 hello DNS 수준에서 작동 한다는입니다.**  트래픽 관리자 사용 하 여 DNS toodirect 클라이언트 toospecific 서비스 hello 트래픽 라우팅 방법의 hello 규칙에 따라 끝점입니다. 클라이언트가 연결 toohello 선택한 끝점 **직접**합니다. Traffic Manager는 프록시 또는 게이트웨이가 아닙니다. 트래픽 관리자는 클라이언트 hello와 hello 서비스 간에 전달 되는 hello 트래픽에 표시 되지 않습니다.

### <a name="traffic-manager-example"></a>트래픽 관리자 예제

Contoso Corp에서 새 파트너 포털을 개발했습니다. 이 포털에 대 한 hello URL https://partners.contoso.com/login.aspx입니다. hello 응용 프로그램은 Azure의 세 가지 영역에서 호스트 됩니다. tooimprove 가용성 전역 성능을 최대화 하 고, 트래픽 관리자 toodistribute 클라이언트 트래픽 toohello 가장 가까운 사용할 수 있는 끝점을 사용 합니다.

tooachieve이이 구성 단계를 수행 하는 hello 완료:

1. 3개의 서비스 인스턴스를 배포합니다. 이러한 배포의 DNS 이름을 hello 'contoso us.cloudapp.net', 'contoso eu.cloudapp.net' 및 'contoso asia.cloudapp.net' 됩니다.
2. 'Contoso.trafficmanager.net' 이라는 트래픽 관리자 프로필을 만들고 hello 세 끝점을 통해 toouse hello 'Performance' 트래픽 라우팅 방법을 구성 합니다.
* 자신의 베 니 티 도메인 이름, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net 구성 '을 DNS CNAME 레코드를 사용 합니다.

![트래픽 관리자 DNS 구성][1]

> [!NOTE]
> Azure 트래픽 관리자는 베 니 티 도메인을 사용 하 여 CNAME toopoint 베 니 티 도메인 이름 tooyour 트래픽 관리자 도메인 이름을 사용 해야 합니다. DNS 표준 허용 하지 않습니다 하면 도메인의 '루트' hello에 CNAME toocreate (또는 루트). 따라서 'contoso.com'('naked' 도메인이라고도 함)에 대한 CNAME을 만들 수 없습니다. 'contoso.com'의 도메인(예: 'www.contoso.com')에 대해서만 CNAME을 만들 수 있습니다. 이 제한 해결 toowork, 예: 'www.contoso.com' '만든 contoso.com' tooan 대체 이름에 대 한 간단한 HTTP 리디렉션 toodirect 요청을 사용 하는 것이 좋습니다.

### <a name="how-clients-connect-using-traffic-manager"></a>트래픽 관리자를 사용하여 클라이언트를 연결하는 방법

클라이언트 hello 페이지 https://partners.contoso.com/login.aspx 요청 hello 앞의 예제에서 계속 실행, hello 클라이언트는 hello 단계 tooresolve hello DNS 이름 다음을 수행 하 고 연결을 설정:

![트래픽 관리자를 사용하여 연결 설정][2]

1. hello 클라이언트는 DNS 쿼리 tooits 구성 된 재귀 DNS 서비스 partners.contoso.com을' tooresolve hello 이름' 보냅니다. '로컬 DNS' 서비스라고도 하는 재귀 DNS 서비스는 DNS 도메인을 직접 호스트하지 않습니다. 대신, 클라이언트 hello off-loads hello 작업 hello에 연결의 다양 한 권한 있는 DNS에서 서비스 hello 필요한 인터넷 tooresolve DNS 이름입니다.
2. tooresolve hello DNS 이름 hello 재귀 DNS 서비스 hello '만든 contoso.com' 도메인에 대 한 hello 이름 서버를 찾습니다. 그런 다음 이러한 이름 서버 toorequest hello 'partners.contoso.com' DNS 레코드 관리자. contoso.com DNS 서버 hello toocontoso.trafficmanager.net 가리키는 hello CNAME 레코드를 반환 합니다.
3. 다음으로 hello 재귀 DNS 서비스는 hello Azure 트래픽 관리자 서비스에서 제공 하는 hello 'trafficmanager.net' 도메인에 대 한 hello 이름 서버를 찾습니다. Hello 'contoso.trafficmanager.net' DNS 레코드 toothose에 대 한 요청 DNS 서버로 다음 전송합니다.
4. 트래픽 관리자 이름 서버 hello hello 요청을 수신 합니다. 다음 항목에 따라 끝점을 선택합니다.

    - 각 끝점의 hello 구성 상태 (비활성화 된 끝점 반환 되지 않습니다.)
    - hello hello 트래픽 관리자 상태를 기준으로 각 끝점의 현재 상태를 확인 합니다. 자세한 내용은 [트래픽 관리자 끝점 모니터링](traffic-manager-monitoring.md)을 참조하세요.
    - 트래픽 라우팅 방법을 선택한 번호입니다. 자세한 내용은 [Traffic Manager 라우팅 메서드](traffic-manager-routing-methods.md)를 참조하세요.

5. DNS CNAME 레코드가 다른 레코드와 선택한 hello 끝점 반환 됩니다. 이 경우에 contoso us.cloudapp.net을 반환한다고 가정하겠습니다.
6. 다음으로 hello 재귀 DNS 서비스는 hello 'cloudapp.net' 도메인에 대 한 hello 이름 서버를 찾습니다. 해당 이름 서버 toorequest hello 'contoso us.cloudapp.net' 접속 DNS 레코드입니다. Hello 미국 기반 서비스 끝점의 hello IP 주소를 포함 하는 DNS 'A' 레코드가 반환 됩니다.
7. hello 재귀 DNS 서비스는 hello 결과 통합 하 고 단일 DNS 응답 toohello 클라이언트를 반환 합니다.
8. hello 클라이언트 hello DNS 결과 받고 toohello IP 주소를 연결 합니다. hello 클라이언트를 통해 트래픽 관리자가 아닌 toohello 응용 프로그램 서비스 끝점을 직접 연결합니다. Hello 클라이언트 hello 필요한 SSL/TLS 핸드셰이크를 수행 하 고이 다음 hello에 대 한 HTTP GET 요청을 만드는 HTTPS 끝점 이므로, ' / login.aspx' 페이지.

hello 재귀 DNS 서비스는 hello DNS 응답을 받으면 캐시 합니다. hello 클라이언트 장치에 hello DNS 확인자 hello 결과 캐시 하기도 합니다. 다른 이름 서버에 쿼리 하는 대신 hello 캐시에서 데이터를 사용 하 여 보다 신속 하 게 응답 하는 후속 DNS 쿼리 toobe를 캐싱은 합니다. hello 캐시의 hello 시간은 각 DNS 레코드의 hello '-time-to-live ' (TTL) 속성에 의해 결정 됩니다. 더 빠른 캐시 만료 및 따라서 왕복 toohello 트래픽 관리자 이름 서버를 더 짧은 값 생성 됩니다. 긴 값 실패 한 끝점에서 멀리 toodirect 트래픽을 더 오래 걸릴 수 있다는 것을 의미 합니다. 트래픽 관리자를 사용 하면 tooconfigure hello TTL 트래픽 관리자 DNS 응답이 toobe 낮은 0 초에서에서 사용 되는 및 최대 2147483647 초 (최대 범위 준수 hello [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), toochoose hello 값 수 있도록 지원 응용 프로그램의 hello 요구를 가장 잘 조정합니다.

## <a name="pricing"></a>가격

가격 책정 정보는 [Traffic Manager 가격 책정](https://azure.microsoft.com/pricing/details/traffic-manager/)을 참조하세요.

## <a name="faq"></a>FAQ

Traffic Manager에 대한 자주 묻는 질문과 답변은 [Traffic Manager FAQ](traffic-manager-FAQs.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

트래픽 관리자 [끝점 모니터링 및 자동 장애 조치(failover)](traffic-manager-monitoring.md)에 대해 자세히 알아봅니다.

트래픽 관리자 [트래픽 라우팅 방법](traffic-manager-routing-methods.md)에 대해 자세히 알아봅니다.

일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png


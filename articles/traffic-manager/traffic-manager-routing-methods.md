---
title: "트래픽 관리자-aaaAzure 트래픽 라우팅 메서드 | Microsoft Docs"
description: "이 문서 hello 다른 트래픽 라우팅 방법 트래픽 관리자에서 사용을 이해 하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>트래픽 관리자 라우팅 방법

Azure 트래픽 관리자 지원 4 트래픽 라우팅 방법 toodetermine 어떻게 tooroute 네트워크 트래픽 toohello 다양 한 서비스 끝점입니다. 트래픽 관리자 hello 트래픽 라우팅 방법을 tooeach DNS 쿼리를 받을 적용 됩니다. hello 트래픽 라우팅을 메서드 hello DNS 응답에 반환 되는 끝점을 결정 합니다.

Traffic Manager에서 사용할 수 있는 네 가지 트래픽 라우팅 메서드가 있습니다.

* **[우선 순위](#priority):** 선택 **우선 순위** 모든 트래픽에 대 한 toouse 기본 서비스 끝점을 선택 하 고 hello 기본 또는 백업 끝점이 hello 사용할 수 없는 경우 백업을 제공 합니다.
* **[가 중](#weighted):** 선택 **가 중** 하려는 경우 toodistribute 트래픽을 끝점 집합에서 하거나 균등 하 게 또는 따라 tooweights 정의 하는 합니다.
* **[성능](#performance):** 선택 **성능** 끝점 서로 다른 지리적 위치에 있는 경우 있고 hello 가장 낮은 네트워크 지연 시간의 측면에서 최종 사용자에 게 toouse hello "가장 가까운" 끝점을 하려는 경우.
* **[지리적](#geographic):** 선택 **지리적** DNS 쿼리에서 제공 되는 지리적 위치에 따라 toospecific 방향이 지정 된 끝점 (Azure, 외부, 또는 중첩) 사용자가 없도록 합니다. 이렇게 하면 트래픽 관리자 고객 tooenable 시나리오 사용자의 지리적 지역을 파악 하 고 그에 따라 라우팅하고 중요 합니다. 데이터 독립성 지시 사항, 콘텐츠 및 사용자 환경의 지역화를 준수하고 다른 지역의 트래픽을 측정하는 작업을 예로 들 수 있습니다.

모든 Traffic Manager 프로필에는 끝점 상태 및 자동 끝점 장애 조치(Failover)의 모니터링이 포함됩니다. 자세한 내용은 [트래픽 관리자 끝점 모니터링](traffic-manager-monitoring.md)을 참조하세요. 단일 트래픽 관리자 프로필은 1가지 트래픽 라우팅 방법만 사용할 수 있습니다. 언제든지 프로필에 대해 다른 트래픽 라우팅 방법을 선택할 수 있습니다. 1분 안에 변경 내용이 적용되며 가동 중지는 발생하지 않습니다. 중첩 트래픽 관리자 프로필을 사용하여 트래픽 라우팅 방법을 결합할 수 있습니다. 중첩 정교 하 고 유연한 트래픽 라우팅 구성을 더 큰 복잡 한 응용 프로그램의 hello 요구를 충족 하는 수 있습니다. 자세한 내용은 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 참조하세요.

## <a name = "priority"></a>우선 순위 트래픽 라우팅 방법

종종 조직 자신의 기본 서비스가 중단 될 경우 하나 이상의 백업 서비스를 배포 하 여 해당 서비스에 대 한 tooprovide 안정성을 하려고 합니다. hello 'Priority' 트래픽 라우팅 메서드를 사용 하면 Azure 고객 tooeasily이 장애 조치 패턴을 구현 합니다.

![Azure Traffic Manager '우선 순위' 트래픽 라우팅 메서드][1]

hello 트래픽 관리자 프로필에는 서비스 끝점의 우선 순위 목록을 포함합니다. 기본적으로 트래픽 관리자는 모든 트래픽을 toohello 기본 (가장 높은 우선 순위) 끝점을 보냅니다. Hello 기본 끝점에 사용할 수 없는 경우 트래픽 관리자 경로 hello 트래픽 toohello 두 번째 끝점입니다. 두 hello 기본 및 보조 끝점을 사용할 수 없는 경우 세 번째로 등과 hello 트래픽은 toohello를 전송 됩니다. Hello 구성 상태 (사용 또는 사용 하지 않도록 설정)를 기반으로 하는 hello 끝점의 가용성 및 지속적인 끝점 모니터링을 hello 합니다.

### <a name="configuring-endpoints"></a>끝점 구성

각 끝점에 대 한 hello 'priority' 속성을 사용 하 여 명시적 hello 끝점 우선 순위를 구성할 Azure 리소스 관리자와 있습니다. 이 속성은 1에서 1000 사이의 값입니다. 값이 낮을수록 더 높은 우선 순위를 나타냅니다. 끝점은 우선 순위 값을 공유할 수 없습니다. Hello 속성을 설정 하는 것은 선택 사항입니다. 생략 하면 hello 끝점 순서에 따라 기본 우선 순위 사용 됩니다.

##<a name = "weighted"></a>가중 트래픽 라우팅 방법
hello '가 중' 트래픽 라우팅 방법을 사용 하면 toodistribute 트래픽을 균등 하 게 또는 toouse 미리 정의 된 가중치입니다.

![Azure Traffic Manager '가중' 트래픽 라우팅 메서드][2]

Hello 가중치가 적용 된 트래픽 라우팅 방법에서 가중치 tooeach 끝점 hello 트래픽 관리자 프로필을 구성에 할당합니다. hello 가중치는 1 too1000 까지의 정수입니다. 이 매개 변수는 선택 사항입니다. 생략되면 Traffic Manager는 '1'이라는 기본 가중치를 사용합니다.

Traffic Manager는 수신한 각 DNS 쿼리에 대해 사용 가능한 끝점을 임의로 선택합니다. 끝점을 선택할 때의 hello 확률 tooall 사용 가능한 끝점을 할당 하는 hello 가중치를 기반으로 합니다. 모든 끝점 결과도 트래픽 배포에 걸쳐 무게 hello를 사용 하 여 동일 합니다. 특정 끝점에서 위 또는 아래로 가중치를 사용 하 여 해당 끝점 toobe 자주 보내거나 가끔 hello DNS 응답에 반환 하면 됩니다.

가 중 hello 메서드를 사용 하면 몇 가지 유용한 시나리오:

* 응용 프로그램의 단계적 업그레이드: 트래픽 tooroute tooa 새 끝점을 백분율로 할당 하 고 시간 too100 %hello 트래픽을 점진적으로 증가 시킵니다.
* 응용 프로그램 마이그레이션 tooAzure: Azure 및 외부 끝점으로 프로필을 만듭니다. Hello 끝점 tooprefer hello 새 끝점의 hello 가중치를 조정 합니다.
* 추가 용량을 위한 클라우드 전환: 신속 하 게 사용 하 여 트래픽 관리자 프로필 뒤 hello 클라우드로 온-프레미스 배포를 확장 합니다. Hello 클라우드에 추가 용량이 필요한 경우 추가 하 고 하거나 더 많은 끝점을 사용 하도록 설정 하 고, 어떤 정도의 트래픽이 향하게 tooeach 끝점 지정 수 있습니다.

hello Azure 리소스 관리자 포털에는 중된 트래픽 라우팅을 hello 구성을 지원합니다.  Hello 리소스 관리자 버전의 Azure PowerShell, CLI 및 hello REST Api를 사용 하 여 가중치를 구성할 수 있습니다.

것이 중요 한 toounderstand DNS 응답이 클라이언트에서 캐시 및 클라이언트 hello hello 재귀 DNS 서버에 의해 tooresolve DNS 이름을 사용 합니다. 이 캐싱은 가중 트래픽 분산에 영향을 줄 수 있습니다. 클라이언트 및 재귀 DNS 서버 hello 수가 큰 경우 트래픽 분배로 인해 예상 대로 작동 합니다. 그러나 hello 클라이언트 또는 재귀 DNS 서버 수가 작을 때 캐싱 수를 상당히 왜곡 시킬 hello 트래픽 분배로 인해 합니다.

일반 사용 사례는 다음과 같습니다.

* 개발 및 테스트 환경
* 응용 프로그램 간 통신
* 일반적인 재귀 DNS 인프라를 공유하는 좁은 사용자 기반을 목표로 하는 응용 프로그램(예: 프록시를 통해 연결하는 회사의 직원)

이러한 DNS 캐싱 효과 일반적인 tooall DNS 기반 트래픽 라우팅 시스템을 뿐 아니라 Azure 트래픽 관리자입니다. 경우에 따라 명시적으로 hello DNS 캐시를 지우는 해결 방법을 제공할 수 있습니다. 대체 트래픽 라우팅 방법이 더 적절한 경우도 있습니다.

## <a name = "performance"></a>성능 트래픽 라우팅 방법

Hello 전세계 둘 이상의 위치에서 끝점을 배포 합니다. '가장 가까운' tooyou 있는 라우팅 트래픽 toohello 위치 하 여 많은 응용 프로그램의 hello 응답성을 향상할 수 있습니다. hello 'Performance' 트래픽 라우팅 메서드는이 기능을 제공합니다.

![Azure Traffic Manager '성능' 트래픽 라우팅 메서드][3]

hello '가장 가까운' 끝점 지리적 거리를 기준으로 가장 가까운 필요 하지 않습니다. 대신, hello 'Performance' 트래픽 라우팅 방법 네트워크 대기 시간을 측정 하 여 hello 가장 가까운 끝점을 결정 합니다. 트래픽 관리자는 인터넷 대기 시간 테이블 tootrack hello 왕복 시간 IP 주소 범위와 각 Azure 데이터 센터 간에 유지 관리합니다.

트래픽 관리자는 hello 인터넷 대기 시간 테이블에서에서 hello 들어오는 DNS 요청의 hello 원본 IP 주소를 찾습니다. 트래픽 관리자는 hello 해당 IP 주소 범위에 대 한 hello 지연이 적습니다 다음 hello DNS 응답에에서 해당 끝점을 반환 하는 Azure 데이터 센터에서에서 사용 가능한 끝점을 선택 합니다.

[Traffic Manager 작동 방식](traffic-manager-overview.md#how-traffic-manager-works)에 설명된 대로 Traffic Manager는 클라이언트에서 직접 DNS 쿼리를 수신하지 않습니다. 대신, DNS 쿼리는 해당 hello 클라이언트는 구성 된 toouse hello 재귀 DNS 서비스에서 제공 됩니다. 따라서 hello IP 주소 사용 toodetermine hello '가장 가까운' 끝점이 있지 않으면 hello 클라이언트의 IP 주소 이지만 hello 재귀 DNS 서비스의 IP 주소 hello 합니다. 실제로이 IP 주소는 클라이언트 hello에 대 한 좋은 프록시.


트래픽 관리자 정기적으로 업데이트의 변경 내용에 대 한 인터넷 대기 시간 테이블 tooaccount hello 글로벌 인터넷 및 새 Azure 지역 hello 합니다. 그러나 응용 프로그램 성능에 따라 다르게 부하의 실시간 변형이 hello 인터넷에서. 성능 트래픽 라우팅은 지정된 서비스 끝점에 대한 부하를 모니터링하지 않습니다. 그러나 끝점을 사용할 수 없는 경우 Traffic Manager는 해당 끝점을 DNS 쿼리 응답에 포함하지 않습니다.


포인트 toonote:

* 프로필에서 여러 끝점을 포함 하는 경우 트래픽 관리자 트래픽을 분산 균등 하 게 해당 지역에서 사용 가능한 끝점 hello 다음 같은 Azure 지역 hello 합니다. 지역 내에서 다른 트래픽 분산을 원하는 경우 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 사용할 수 있습니다.
* 모든 끝점에 가장 가까운 hello 사용 하는 경우 Azure 지역 저하 됩니다, 그리고 트래픽 관리자 hello 다음 가장 가까운 Azure 지역에 트래픽을 toohello 끝점을 이동 합니다. 기본 장애 조치 순서 toodefine 사용 [트래픽 관리자 프로필을 중첩](traffic-manager-nested-profiles.md)합니다.
* Hello 성능 트래픽 라우팅 방법을 외부 끝점 또는 중첩 된 끝점을 사용할 경우 해당 끝점의 toospecify hello 위치를 해야 합니다. Hello Azure 지역 가장 가까운 tooyour 배포를 선택 합니다. 이러한 위치는 hello 인터넷 대기 시간 테이블에서 지 원하는 hello 값입니다.
* hello 끝점을 선택 하는 hello 알고리즘은 결정적입니다. 동일한 클라이언트는 hello에서 DNS 쿼리 전송 toohello 반복 동일한 끝점입니다. 일반적으로 클라이언트는 이동할 때 다른 재귀 DNS 서버를 사용합니다. 클라이언트 hello 라우트된 tooa 다른 끝점 수 있습니다. 라우팅도 영향을 받을 수 업데이트 toohello 인터넷 대기 시간 테이블입니다. 따라서 성능 트래픽 라우팅을 메서드는 클라이언트는 항상 보증 하지 않습니다 hello 라우팅된 toohello 동일한 끝점입니다.
* 인터넷 대기 시간 테이블 hello 변경 될 때 해당 일부 클라이언트는 방향이 지정 된 tooa 다른 끝점을 확인할 수 있습니다. 이 라우팅 변경 내용은 현재 대기 시간 데이터에 따라 더 정확합니다. 이러한 업데이트는 성능 트래픽 라우팅 인터넷 계속 발전 hello로의 필수 toomaintain hello 정확도 합니다.

## <a name = "geographic"></a>지리적 트래픽 라우팅 방법

트래픽 관리자 프로필에 구성 된 toouse hello에서 지리 toospecific 끝점 (Azure, 외부 또는 중첩)가 DNS 쿼리에서 지리적 위치에 따라 사용자가 보내지는지 있도록 메서드 라우팅이 발생 될 수 있습니다. 이렇게 하면 트래픽 관리자 고객 tooenable 시나리오 사용자의 지리적 지역을 파악 하 고 그에 따라 라우팅하고 중요 합니다. 데이터 독립성 지시 사항, 콘텐츠 및 사용자 환경의 지역화를 준수하고 다른 지역의 트래픽을 측정하는 작업을 예로 들 수 있습니다.
프로필은 지리적 라우팅을 위해 구성 된, 각 끝점 연결 된 프로필에 할당 된 지역 tooit 집합이 toohave 필요 함을. 지리적 지역은 다음과 같은 수준으로 세분화될 수 있습니다. 
- 세계–모든 지역
- 지역 그룹화 - 예: 아프리카, 중동, 오스트레일리아/태평양 등 
- 국가/지역 - 예: 아일랜드, 페루, 홍콩 특별 행정구 등 
- 시/도 - 예: 미국-캘리포니아, 오스트레일리아-퀸즐랜드, 캐나다-앨버타 등(참고: 이 세분성 수준은 오스트레일리아, 캐나다, 영국 및 미국의 주/지방에서만 지원됨).

영역 또는 영역 집합 tooan 끝점 할당 된 경우 해당 영역에서 모든 요청 라우트된만 toothat 끝점을 가져옵니다. 트래픽 관리자는 hello hello DNS 쿼리 toodetermine hello 영역 있는 사용자는 쿼리 하는 – 일반적으로이 hello hello 사용자를 대신 하 여 hello 쿼리를 수행 하는 로컬 DNS 확인자의 hello IP 주소가 원본 IP 주소를 사용 합니다.  

![Azure Traffic Manager '지리적' 트래픽 라우팅 메서드](./media/traffic-manager-routing-methods/geographic.png)

트래픽 관리자 DNS 쿼리 hello hello 원본 IP 주소를 읽고 어떤 지역에서 발생 하는 것을 결정 합니다. 그런 다음이 지역 매핑된 tooit을 가진 끝점을 없을 경우 toosee를 찾습니다. 이 조회 hello 최하위 세분성 수준 (시/도는, 그렇지 않으면 hello 국가/지역 수준에서)에서 시작 나타나고 모든 hello 반복 해 toohello 최고 수준인 **세계**합니다. hello 첫 번째 일치 항목이이 이동이를 사용 하 여 hello 끝점 tooreturn hello 쿼리 응답에 지정 합니다. 중첩 형식 끝점과 일치하는 경우 해당 라우팅 방법을 기준으로 자식 프로필 내의 끝점이 반환됩니다. hello 포인트 다음은 적용 가능한 toothis 동작입니다.

- 지리적인 지역의 지리적 라우팅 hello 라우팅 형식이 때 트래픽 관리자 프로필에서 매핑된 전용 tooone 끝점 수 있습니다. 이렇게 하면 사용자 라우팅이 결정적이며 고객이 모호하지 않은 지리적 경계가 필요한 시나리오를 사용할 수 있습니다.
- 사용자의 지역 지리적 매핑 아래에서 두 개의 다른 끝점의 경우, 트래픽 관리자는 hello 최소 단위 hello 끝점을 선택 하 고 해당 지역 toohello의 라우팅 요청을 다른 끝점을 고려 하지 않습니다. 예를 들어 Endpoint1과 Endpoint2라는 두 개의 끝점이 있는 지리적 라우팅 형식 프로필을 고려해 보세요. Endpoint1 구성 된 tooreceive 트래픽이 아일랜드 및 Endpoint2에서 구성 된 유럽에서 tooreceive 트래픽을 합니다. 요청 아일랜드에서 시작, 경우 항상 라우트된 tooEndpoint1입니다.
- 영역 매핑된 전용 tooone 끝점 수 있으므로, 트래픽 관리자 끝점 hello 정상 인지 여부에 관계 없이 반환 됩니다.

    >[!IMPORTANT]
    >Hello 지리적 라우팅 메서드를 사용 하는 고객 연결할 수 있도록 hello 중첩 형식 끝점을 자식 프로필을 각각 내에서 두 개 이상의 끝점을 포함 하는 것이 좋습니다.
- 끝점 일치 하는 항목이 고 hello에 해당 끝점은 **Stopped** 상태 이면 트래픽 관리자 NODATA 응답을 반환 합니다. 이 경우 더 이상 없는 조회 hello 지리적 영역 계층 구조에서 올리십시오 설정 됩니다. 이 동작은 hello 자식 프로필 hello 중인 경우에 중첩된 끝점 유형에 적용 됩니다 **Stopped** 또는 **비활성화** 상태입니다.
- 끝점을 표시 하는 경우는 **비활성화 된** 상태, 일치 하는 프로세스는 hello 영역에 포함 되지 않습니다. 이 동작은 hello 끝점 hello 중인 경우에 중첩된 끝점 유형에 적용 됩니다 **비활성화** 상태입니다.
- 쿼리가 해당 프로필에 매핑이 없는 지리적 지역에서 수행된 경우 Traffic Manager는 NODATA 응답을 반환합니다. 따라서 하는 것이 좋습니다을 사용 하는 하나의 끝점에 이상적 형식의 중첩 hello 영역과 hello 자식 프로필 내에 적어도 두 개의 끝점으로 지리적 라우팅 **세계** tooit를 할당 합니다. 이렇게 하면 tooa 영역에 매핑되지 않는 모든 IP 주소 처리 됩니다.

[Traffic Manager 작동 방식](traffic-manager-how-traffic-manager-works.md)에 설명된 대로 Traffic Manager는 클라이언트에서 직접 DNS 쿼리를 수신하지 않습니다. 대신, DNS 쿼리는 해당 hello 클라이언트는 구성 된 toouse hello 재귀 DNS 서비스에서 제공 됩니다. 따라서 hello IP 주소 사용 toodetermine hello 지역 클라이언트의 IP 주소를 hello 이지만 hello 재귀 DNS 서비스의 IP 주소 hello 하지 않습니다. 실제로이 IP 주소는 클라이언트 hello에 대 한 좋은 프록시.


## <a name="next-steps"></a>다음 단계

자세한 방법을 사용 하 여 고가용성 응용 프로그램 toodevelop [트래픽 관리자 끝점 모니터링](traffic-manager-monitoring.md)

너무 방법에 대해 알아봅니다[트래픽 관리자 프로필 만들기](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png




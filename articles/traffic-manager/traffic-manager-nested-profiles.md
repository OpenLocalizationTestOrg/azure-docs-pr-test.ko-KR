---
title: "트래픽 관리자 프로필 aaaNested | Microsoft Docs"
description: "이 문서에서는 Azure 트래픽 관리자의 hello 중첩 프로필 기능 설명"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>중첩 트래픽 관리자 프로필

트래픽 관리자 끝점 각 최종 사용자 로부터 트래픽을 받아야 트래픽 관리자가 선택 하는 방법 toocontrol 사용할 수 있는 트래픽 라우팅 메서드가의 범위에 포함 됩니다. 자세한 내용은 [트래픽 관리자 트래픽 라우팅 방법](traffic-manager-routing-methods.md)을 참조하세요.

각 트래픽 관리자 프로필은 단일 트래픽 라우팅 방법을 지정합니다. 그러나 단일 트래픽 관리자 프로필에서 제공 hello 라우팅 보다 더 정교한 트래픽 라우팅이 필요로 하는 시나리오가 있습니다. 둘 이상의 트래픽 라우팅 방법의 트래픽 관리자 프로필 toocombine hello 혜택을 중첩할 수 있습니다. 중첩 된 프로필을 사용 하면 더 큰 toooverride hello 기본 트래픽 관리자 동작 toosupport 및 더 복잡 한 응용 프로그램 배포.

다음 예제는 hello toouse 다양 한 시나리오에서 트래픽 관리자 프로필을 중첩 하는 방법을 보여 줍니다.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>예제 1: '성능' 및 '가중' 트래픽 라우팅 결합

Azure 지역에 따라 hello에서 응용 프로그램을 배포 하는 가정: 미국 서 부, 서 부 유럽 및 아시아 합니다. 트래픽 관리자의 'Performance' 트래픽 라우팅 메서드 toodistribute 트래픽 toohello 지역 가장 가까운 toohello 사용자를 사용할 수 있습니다.

![단일 트래픽 관리자 프로필][4]

이제, 원하는 tootest 업데이트 tooyour 서비스 배포 전에 더 광범위 하 게 가정해 봅니다. Toouse hello 'weighted' 트래픽 라우팅 방법 toodirect 트래픽 tooyour 테스트 배포의 작은 비율을 사용 하는 것이 좋습니다. 서 부 유럽에서 hello 기존 프로덕션 배포와 함께 hello 테스트 배포를 설정 합니다.

단일 프로필에서 '가중' 및 '성능' 트래픽 라우팅을 결합할 수 없습니다. toosupport hello 두 서 부 유럽 끝점 및 hello '가 중' 트래픽 라우팅 메서드를 사용 하 여 트래픽 관리자 프로필을 만들면이 시나리오에서는 합니다. 다음으로, 끝점 toohello 'parent' 프로필로이 'child' 프로필을 추가합니다. 다른 글로벌 배포 끝점으로 hello 하는 hello 부모 프로필 여전히 사용 하 여 성능 트래픽 라우팅 방법 hello 및를 포함 합니다.

hello 다음 다이어그램에서는이 예제를 보여 줍니다.

![중첩 트래픽 관리자 프로필][2]

이 구성에서는 hello 부모 프로필을 통해 보내지는 트래픽을 트래픽을 분산 영역 정상적으로 합니다. 서 부 유럽 내 hello 중첩된 프로필 배포 트래픽 toohello 프로덕션 환경과 테스트 끝점 toohello 가중치 할당에 따라 합니다.

Hello 부모 프로필 hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우 각 끝점 위치를 할당 되어야 합니다. hello 위치는 hello 끝점을 구성할 때 지정 됩니다. Hello Azure 지역 가장 가까운 tooyour 배포를 선택 합니다. hello Azure 영역은 hello 인터넷 대기 시간 테이블에서 지 원하는 hello 위치 값입니다. 자세한 내용은 [Traffic Manager '성능' 트래픽 라우팅 메서드](traffic-manager-routing-methods.md#performance)를 참조하세요.

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>예제 2: 중첩 프로필의 끝점 모니터링

트래픽 관리자는 각 서비스 끝점의 hello 상태를 적극적으로 모니터링 합니다. 끝점 상태가 정상이 아닌 경우 서비스의 사용자가 tooalternative 끝점 toopreserve hello 가용성 트래픽 관리자에 지시 합니다. 이 끝점 모니터링 및 장애 조치 동작 tooall 트래픽 라우팅 메서드를 적용합니다. 자세한 내용은 [트래픽 관리자 끝점 모니터링](traffic-manager-monitoring.md)을 참조하세요. 끝점 모니터링은 중첩 프로필에 대해 다르게 작동합니다. 중첩 된 프로필을 통해 hello 부모 프로필에서 hello 자식에 대해 상태 검사를 직접 수행 하지 않습니다. 대신 hello 자식 프로필의 끝점의 hello 상태는 사용 되는 toocalculate hello hello 자식 프로필의 전반적인 상태입니다. 이 상태 정보는 중첩 된 hello 프로필 계층 구조를 전파 됩니다. hello 부모 프로필이 사용 합니다.이 집계 상태 toodetermine 여부 toodirect 트래픽 toohello 자식 프로필입니다. Hello 참조 [FAQ](traffic-manager-FAQs.md#traffic-manager-nested-profiles) 대 한 자세한 내용은 중첩 된 프로필의 상태를 모니터링 합니다.

서 부 유럽에서 hello 프로덕션 배포에 실패 가정 toohello 앞의 예제를 반환 합니다. 기본적으로 hello 'child' 프로필에서는 모든 트래픽이 toohello 테스트 배포를 안내합니다. Hello 테스트 배포도 실패 하는 경우는 hello 자식 프로필을 받지 않는 트래픽 정상 상태가 아닌 모든 자식 끝점 이후 hello 부모 프로필 결정 합니다. 그런 다음 부모 프로필 hello 다른 지역의 트래픽 toohello를 배포합니다.

![중첩 프로필 장애 조치(기본 동작)][3]

이 정렬에 만족할 수 있습니다. 또는 서 부 유럽에 대 한 모든 트래픽이 제한 된 하위 집합 트래픽 대신 toohello 테스트 배포 이제 문제가 발생할 수 있습니다. Hello의 hello 상태에 관계 없이 테스트 배포, toofail 통해 하려는 toohello 다른 지역에 서 부 유럽 hello 프로덕션 배포에 실패 하는 경우. tooenable이 장애이 조치 hello 부모 프로필에서 끝점으로 hello 자식 프로필을 구성할 때 hello 'MinChildEndpoints' 매개 변수를 지정할 수 있습니다. hello 매개 변수는 hello hello 자식 프로필에서 사용할 수 있는 끝점의 최소 수를 결정합니다. hello 기본값은 '1'입니다. 이 시나리오에 대 한 hello MinChildEndpoints 값 too2를 설정할 수 있습니다. 이 임계값 아래로 hello 부모 프로필 hello 전체 자식 프로필 toobe를 사용할 수 없는 것으로 간주 하 고 트래픽을 toohello 다른 끝점을 보냅니다.

hello 다음 그림에서는이 구성을 수행 합니다.

!['MinChildEndpoints' = 2인 중첩 프로필 장애 조치][4]

> [!NOTE]
> 모든 트래픽 tooa 단일 끝점을 배포 하는 hello 'Priority' 트래픽 라우팅 방법. 따라서 하위 프로필의 경우 MinChildEndpoints '1'이 아닌 값을 설정합니다.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>예제 3: '성능' 트래픽 라우팅에서 우선 순위가 지정된 장애 조치(Failover) 지역

hello 기본 hello 'Performance' 트래픽 라우팅 방법에 대 한 동작은 설계 된 tooavoid 과도 하 게 끝점에 가장 가까운 hello 다음 로드 및 연계 일련의 오류가 발생 합니다. 끝점에 실패 하면가 지시한 toothat 끝점을 균등 하 게 하는 모든 트래픽을 분산 toohello 다른 끝점 모든 지역.

![기본 장애 조치를 사용하는 '성능' 트래픽 라우팅][5]

그러나 두 끝점 모두 사용할 수 없을 때 트래픽을 tooother 영역 직접와 hello 서 부 유럽 트래픽 장애 조치 tooWest US, 원하는 가정 합니다. 자식 프로필 hello 'Priority' 트래픽 라우팅 메서드를 사용 하 여이 솔루션을 만들 수 있습니다.

![기본 설정 장애 조치를 사용하는 '성능' 트래픽 라우팅][6]

Hello 서 부 유럽 끝점 hello West US 끝점 보다 높은 우선 순위에 있으므로는 모든 트래픽이 양쪽 끝점이 온라인 상태일 때 toohello 서 부 유럽 끝점에 전송 됩니다. 서 부 유럽에 실패 하면 해당 트래픽은 directed tooWest 미국입니다. 중첩 된 hello 프로필을 트래픽은 서 부 유럽 및 West US 모두 실패 하는 경우에 리디렉션된 tooEast 아시아입니다.

모든 지역에 대해 이 패턴을 반복할 수 있습니다. 대체 hello 부모 프로필에 세 개 끝점이 모두 세 개의 자식 프로필 각각 우선 순위가 지정 된 장애 조치 순서를 제공 합니다.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>예 4: hello에서 여러 끝점 간에 동일한 라우팅 'Performance' 트래픽 제어 영역

Hello 'Performance' 트래픽 라우팅 방법을 특정 지역에 대 한 둘 이상의 끝점이 있는 프로필 사용을 가정 합니다. 기본적으로 트래픽은 toothat 영역 해당 지역에서 사용할 수 있는 모든 끝점에서 동시에 균등 향합니다.

![지역 내 트래픽 분산의'성능' 트래픽 라우팅(기본 동작)][7]

유럽 서부에 있는 여러 끝점을 추가하는 대신 해당 끝점을 별도 하위 프로필에서 묶습니다. hello 자식 프로필 toohello 부모 hello만 끝점 서 부 유럽에 추가 됩니다. hello 자식 프로필에 hello 설정은 해당 지역 내에서 우선 순위 기반 또는 가중치가 적용 된 트래픽 라우팅을 사용 하 여 서 부 유럽와 hello 트래픽 분배로 인해를 제어할 수 있습니다.

![사용자 지정 지역 내 트래픽 분산을 사용하는 '성능' 트래픽 라우팅][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>예제 5: 끝점 기준 모니터링 설정

사용 하는 경우를 가정해 볼 트래픽 관리자 toosmoothly 레거시 온-프레미스 웹 사이트 tooa 새로운 클라우드 기반 버전에서 Azure에 호스트 트래픽을 마이그레이션합니다. Hello 레거시 사이트에 대 한 toouse hello 홈 페이지 URI toomonitor 사이트 상태를 할 수 있습니다. Hello 새 버전을 위한 클라우드 기반을 구현 하는 사용자 지정 모니터링 페이지 하지만 (경로가 ' / monitor.aspx') 추가 검사를 포함 하는 합니다.

![트래픽 관리자 끝점 모니터링(기본 동작)][9]

트래픽 관리자 프로필의 모니터링 설정을 hello tooall 끝점 단일 프로필 내에서 적용 됩니다. 중첩 된 프로필을 통해 모니터링 설정을 다른 사이트 toodefine 당 다른 자식 프로필을 사용 합니다.

![끝점 기준 설정을 사용하는 트래픽 관리자 끝점 모니터링][10]

## <a name="next-steps"></a>다음 단계

[Traffic Manager 프로필](traffic-manager-overview.md)에 대한 자세한 정보

너무 방법에 대해 알아봅니다[트래픽 관리자 프로필 만들기](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png

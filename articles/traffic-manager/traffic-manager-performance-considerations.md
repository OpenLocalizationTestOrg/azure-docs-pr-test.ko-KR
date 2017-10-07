---
title: "aaaPerformance 고려 사항에 대 한 Azure 트래픽 관리자 | Microsoft Docs"
description: "트래픽 관리자 성능 이해 및 방법을 트래픽 관리자를 사용 하는 경우 웹 사이트의 tootest 성능"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Traffic Manager 성능 고려 사항

이 페이지에서는 Traffic Manager를 사용할 때의 성능 고려 사항에 대해 설명합니다. Hello를 시나리오를 따르는 것이 좋습니다.

Hello WestUS에서에서 웹 사이트의 인스턴스 및 한국 우편 영역 있는데 트래픽 관리자 프로브 hello에 대 한 hello 상태 검사를 실패 hello 인스턴스 중 하나입니다. 응용 프로그램 트래픽은 directed toohello 정상 영역입니다. 이 장애 조치가 발생할 수 있지만 성능이 이제 tooa 떨어져 있는 영역을 이동 하는 hello 트래픽의 hello 대기 시간에 따라 문제가 될 수 있습니다.

## <a name="performance-considerations-for-traffic-manager"></a>Traffic Manager 성능 고려 사항

hello만 성능에 미치는 영향 트래픽 관리자 수 웹 사이트는 hello 초기 DNS 조회입니다. 트래픽 관리자 프로필의 hello 이름에 대 한 DNS 요청은 해당 호스트 hello trafficmanager.net 영역 hello Microsoft DNS 루트 서버에서 처리 됩니다. 트래픽 관리자 채우고 hello Microsoft DNS 루트 서버 hello 트래픽 관리자 정책 및 hello 검색 결과에 따라, 정기적으로 업데이트 합니다. Hello 초기 DNS 조회 하는 동안에 DNS 쿼리가 더 이상 관리자 tooTraffic 전송 됩니다.

트래픽 관리자는 여러 가지 구성 요소로 이루어진: DNS 서버, API 서비스, hello 저장소 계층 및 모니터링 서비스 끝점 이름입니다. 트래픽 관리자 서비스 구성 요소에 실패 하면 트래픽 관리자 프로필에 연결 된 hello DNS 이름에 영향을 주지 않습니다. hello 레코드 hello Microsoft DNS 서버에서 변경 되지 않습니다. 그러나 끝점 모니터링 및 DNS 업데이트는 일어나지 않습니다. 따라서 트래픽 관리자는 하지 수 tooupdate DNS toopoint tooyour 장애 조치 사이트 기본 사이트가 중단 되 면 합니다.

DNS 이름 확인은 신속하고 결과는 캐시됩니다. hello 초기 DNS 조회의 hello 속도 이름 확인을 위해 사용 하 여 DNS 서버 hello 클라이언트 hello에 따라 달라 집니다. 일반적으로 클라이언트는 50ms 이내에 DNS 조회를 완료할 수 있습니다. hello 조회의 hello 결과의 DNS-time-to-live (TTL) hello hello 기간에 대 한 캐시 됩니다. hello 기본 트래픽 관리자에 대 한 TTL은 300 초입니다.

트래픽은 Traffic Manager를 통해 전달되지 않습니다. Hello DNS 조회 완료 되 면 hello 클라이언트 웹 사이트의 인스턴스에 대 한 IP 주소를 있습니다. hello 클라이언트 toothat 주소에 직접 연결 하 고 트래픽 관리자를 통해 전달 하지 않습니다. 트래픽 관리자 정책을 선택 하면 hello에 hello DNS 성능에 영향을 주지 않습니다. 그러나 성능 라우팅 방법 hello 응용 프로그램 환경이 저하 될 수 있습니다. 예를 들어 정책에 아시아에서 호스팅되는 북미 지역 tooan 인스턴스에서 트래픽을 리디렉션합니다, 하는 경우 해당 세션에 대 한 hello 네트워크 대기 시간 성능 문제를 수 있습니다.

## <a name="measuring-traffic-manager-performance"></a>Traffic Manager 성능 측정

여러 웹 사이트 toounderstand hello 성능 및 트래픽 관리자 프로필의 동작을 사용할 수 있습니다. 이러한 대다수의 사이트는 무료이지만 제한이 있을 수도 있습니다. 일부 사이트는 유료로 향상된 모니터링 및 보고를 제공합니다.

이러한 사이트에 hello 도구 DNS 대기 시간을 측정 하 고 디스플레이 hello hello 전 세계 클라이언트 위치에 대 한 IP 주소를 해결 합니다. 대부분의이 도구는 hello DNS 결과 캐시 하지 않습니다. 따라서 hello 도구는 테스트를 실행할 때마다 hello 전체 DNS 조회를 표시 합니다. 사용자 고유의 클라이언트에서 테스트 하는 경우 hello 전체 DNS 조회 성능을 hello TTL 기간 동안 한 번만 발생 합니다.

## <a name="sample-tools-toomeasure-dns-performance"></a>샘플 도구 toomeasure DNS 성능

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS는 많은 성능 도구를 제공합니다. hello DNS 비교 도구 시간 tooresolve DNS 이름 및 tooother DNS 서비스 공급자를 비교 하는 방법을 확인할 수 있습니다.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Hello 가장 간단한 도구 중 하나는 WebSitePulse 합니다. Hello URL toosee DNS 확인 시간, 첫 번째 바이트, 마지막 바이트 및 기타 성능 통계를 입력 합니다. 3개의 서로 다른 테스트 위치를 선택할 수 있습니다. 이 예제에서는 첫 번째 실행 hello 0.204 sec DNS 조회를 사용 한다고 표시 되는지 확인할 수 있습니다.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Hello 결과가 캐시 되므로 hello에 대 한 두 번째 테스트 hello 같은 트래픽 관리자 끝점 hello DNS 조회 때문에 0.002 초를 사용 합니다.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA 앱 가상 모니터](https://asm.ca.com/en/checkit.php)

    이전 hello Watchmouse 검사 웹 사이트 도구에는,이 사이트 알려주는 동시에 여러 지리적 지역에서 시간 hello DNS 확인 합니다. 여러 지리적 위치에서 hello URL toosee DNS 확인 시간, 연결 시간 및 속도 입력 합니다. 이 테스트 toosee 반환 되는 호스팅된 서비스를 사용 하 여 hello 전 세계 여러 위치에 대 한.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    이 도구는 웹 페이지의 각 요소에 대한 성능 통계를 제공합니다. hello 페이지 분석 탭 DNS 조회에 소요 된 시간의 hello 백분율을 보여 줍니다.

* [Azure DNS란?](http://www.whatsmydns.net/)

    이 사이트에서 DNS 조회 20 개의 다른 위치에서 상속 되지 않습니다 하 고 지도에 hello 결과 표시 합니다.

* [Dig 웹 인터페이스](http://www.digwebinterface.com)

    이 사이트에서는 CNAME 및 A 기록을 포함한 보다 자세한 DNS 정보를 보여줍니다. 옵션에서 '색상화 출력' hello 및 '통계'를 확인 하 고 이름 서버에서 '모두'를 선택 해야 합니다.

## <a name="next-steps"></a>다음 단계

[Traffic Manager 트래픽 라우팅 방법 정보](traffic-manager-routing-methods.md)

[Traffic Manager 설정 테스트](traffic-manager-testing-settings.md)

[Traffic Manager 작업(REST API 참조)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager cmdlet](http://go.microsoft.com/fwlink/p/?LinkId=400769)


---
title: "aaaAzure 트래픽 관리자 끝점 모니터링 | Microsoft Docs"
description: "트래픽 관리자 끝점 모니터링 및 끝점 자동 장애 조치 toohelp Azure 사용 하는 방법을 이해 하는 데이 문서가 도움이 수 가용성이 높은 응용 프로그램을 배포 하는 고객"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Traffic Manager 끝점 모니터링

Azure Traffic Manager에는 기본 제공된 끝점 모니터링 및 자동 끝점 장애 조치가 포함됩니다. 이 기능을 사용 하 여 Azure 지역 실패를 포함 하 여 복원 력 있는 tooendpoint 오류가 있는 가용성이 높은 응용 프로그램을 제공할 수 있습니다.

## <a name="configure-endpoint-monitoring"></a>끝점 모니터링 구성

tooconfigure 끝점 모니터링 hello에 나오는 설정에 따라 트래픽 관리자 프로필을 지정 해야 합니다.

* **프로토콜**. HTTP, HTTPS 또는 TCP으로 선택 트래픽 관리자 끝점 toocheck를 검색할 때 사용 하는 hello 프로토콜의 상태입니다. HTTPS 모니터링 해도 해당 hello 검사-유효한 SSL 인증서가 있는지 여부를 확인 하지 않으므로 인증서가 있습니다.
* **포트**. Hello 요청에 사용 되는 hello 포트를 선택 합니다.
* **경로**. 이 구성 설정을 지정 하 여 hello 경로 설정을 반드시 hello HTTP 및 HTTPS 프로토콜에 대해서만 유효 합니다. Hello TCP 모니터링 프로토콜 오류가 발생에 대해이 설정을 제공합니다. TCP 프로토콜에 대 한 hello 상대 경로 및 제공 hello 웹 페이지 또는 hello 파일의 hello 이름을 해당 hello 액세스를 모니터링 합니다. 슬래시 (/)은 유효한 항목 hello 상대 경로입니다. 이 값 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.
* **검색 간격**. 이 값은 Traffic Manager 검색 에이전트에서 끝점의 상태를 검사하는 빈도를 지정합니다. 여기서 30초(일반 검색) 및 10초(빠른 검색)의 두 값을 지정할 수 있습니다. 지정 된 값이 없으면 hello 프로필 30 초의 tooa 기본값을 설정 합니다. Hello 방문 [트래픽 관리자 가격 책정](https://azure.microsoft.com/pricing/details/traffic-manager) 빠른 검색 가격에 대 한 더 많은 페이지 toolearn 합니다.
* **허용되는 오류 수** 이 값은 Traffic Manager 검색 에이전트가 해당 끝점을 비정상 상태로 표시하기 전에 허용하는 오류 수를 지정합니다. 해당 값의 범위는 0에서 9 사이일 수 있습니다. 값이 0 이면 단일 모니터링 오류 비정상으로 표시 하는 끝점 toobe를 발생할 수 있습니다. 없는 값을 지정 하는 경우 3의 hello 기본값을 사용 합니다.
* **모니터링 제한 시간**. 이 속성의 상태 검사 검색 toohello 끝점에 전송 될 때 오류를 확인 하는 트래픽 관리자 검색 에이전트 고려 하기 전에 대기할 시간 hello hello 크기를 지정 합니다. 이면 too30 초 다음 검색 간격을 설정 하는 hello 5-10 초 사이의 hello 제한 시간 값을 설정할 수 있습니다. 값을 지정하지 않으면 기본값 10초가 사용됩니다. 이면 too10 초 다음 검색 간격을 설정 하는 hello 5에서 9 초 사이의 hello 제한 시간 값을 설정할 수 있습니다. 제한 시간 값을 지정하지 않으면 기본값 9초가 사용됩니다.

![Traffic Manager 끝점 모니터링](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**그림 1: Traffic Manager 끝점 모니터링**

## <a name="how-endpoint-monitoring-works"></a>끝점 모니터링의 작동 방식

프로토콜을 모니터링 하는 hello HTTP 또는 HTTPS로 설정 되어 hello 트래픽 관리자 검색 에이전트는 hello 프로토콜, 포트 및 지정한 상대 경로 사용 하는 GET 요청 toohello 끝점을 만듭니다. 200-OK 응답이 반환되면 해당 끝점은 정상 상태로 간주됩니다. 또는 hello 응답이 다른 값을 지정 하는 hello 제한 시간 내에 수신 된 응답이 없는 경우, hello 트래픽 관리자 에이전트를 검색 합니다. 다시 시도 (없음 다시 시도 작업을 마쳤으면이 설정을 0 이면) toohello 실패의 수 트랜잭션당 설정에 따라 . 연속 실패 횟수 hello hello 실패의 수 트랜잭션당 설정 보다 높은 경우 해당 끝점이 비정상으로 표시 됩니다. 

TCP 프로토콜을 모니터링 하는 hello을 사용 하는 경우 hello 트래픽 관리자 검색 에이전트는 지정 된 hello 포트를 사용 하 여 TCP 연결 요청을 시작 합니다. Hello 끝점 응답 toohello 요청 응답 tooestablish hello 연결을 통해 상태 검사를 성공으로 표시 되어 및 hello 트래픽 관리자 검색 에이전트 hello TCP 연결이 다시 설정 합니다. 다른 값을가 하는 hello 응답 또는 내에서 수신 된 응답이 없는 경우 hello 제한 시간 지정 hello toohello 실패의 트랜잭션당 수 설정 (다시 시도 하지는이 설정을 0 이면)에 따라 트래픽 관리자 에이전트를 검색 합니다. 다시 시도 합니다. 연속 실패 횟수 hello hello 실패의 수 트랜잭션당 설정 보다 크면 해당 끝점이 비정상으로 표시 됩니다.

모든 경우에 여러 위치에서 트래픽 관리자를 조사 하 고 각 지역 내에서 발생 하는 hello 연속 된 실패를 결정 합니다. 즉, 끝점은 받게 됨 상태 검색이 트래픽 관리자에서 검색 간격에 사용 되는 hello 설정 보다 높은 빈도로 합니다.

>[!NOTE]
>HTTP 또는 HTTPS 프로토콜을 모니터링에 대 한 일반적인 hello 끝점 쪽 방법은 tooimplement 응용 프로그램-예를 들어 /health.aspx 내에서 사용자 지정 페이지입니다. 이 경로를 모니터링에 사용하여 성능 카운터 검사 또는 데이터베이스 가용성 확인과 같은 응용 프로그램별 검사를 수행할 수 있습니다. 이러한 사용자 지정 검사에 따라, hello 페이지는 적절 한 HTTP 상태 코드를 반환 합니다.

Traffic Manager 프로필의 모든 끝점은 모니터링 설정을 공유합니다. 만들 수 있습니다 toouse를 서로 다른 끝점에 대 한 모니터링 설정을 다른 해야 할 경우 [트래픽 관리자 프로필을 중첩](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings)합니다.

## <a name="endpoint-and-profile-status"></a>끝점 및 프로필 상태

Traffic Manager 프로필 및 끝점을 사용하거나 사용하지 않도록 설정할 수 있습니다. 그러나 Traffic Manager의 자동 설정 및 프로세스에 따라 끝점 상태가 변경될 수도 있습니다.

### <a name="endpoint-status"></a>끝점 상태

특정 끝점을 사용하거나 사용하지 않도록 설정할 수 있습니다. hello 기본 서비스에 있는 경우일 수 정상, 영향을 받지 않습니다. 변경 hello 끝점 상태 컨트롤 hello hello 트래픽 관리자 프로필에서에서 hello 끝점의 가용성입니다. 끝점 상태를 사용 하지 않도록 설정 하는 경우 트래픽 관리자가 해당 상태를 확인 하지 및 hello 끝점 DNS 응답에 포함 되지 않습니다.

### <a name="profile-status"></a>프로필 상태

Hello 프로필 상태 설정을 사용 하거나 설정할 수 있습니다 특정 프로필을 사용 하지 않도록 설정 합니다. 끝점 상태는 단일 끝점에 영향을 주는 동안 프로필 상태 모든 끝점을 포함 하는 hello 전체 프로필을 영향을 줍니다. 프로필을 사용 하지 않도록 설정 하면 hello 끝점 상태에 대 한 확인 되지 않습니다 하 고 끝점을 하나도 DNS 응답에 포함 됩니다. [NXDOMAIN](https://tools.ietf.org/html/rfc2308) hello DNS 쿼리에 대 한 응답 코드가 반환 됩니다.

### <a name="endpoint-monitor-status"></a>끝점 모니터 상태

끝점 모니터 상태 hello 끝점의 hello 상태를 표시 하는 트래픽 관리자에서 생성 된 값입니다. 이 설정은 수동으로 변경할 수 없습니다. hello 끝점 모니터 상태는 끝점 모니터링의 hello 결과의 조합 및 hello 구성 된 끝점 상태입니다. 끝점 모니터 상태의 hello 가능한 값은 다음 표에 hello에 나와 있습니다.

| 프로필 상태 | 끝점 상태 | 끝점 모니터 상태 | 참고 사항 |
| --- | --- | --- | --- |
| 사용 안 함 |사용 |비활성 |hello 프로필에 사용할 수 없습니다. Hello 끝점 상태 활성화 되어 있지만 hello 프로필 상태 (사용 안 함) 우선적으로 적용 합니다. Disabled 프로필의 끝점은 모니터링되지 않습니다. Hello DNS 쿼리에 대 한 NXDOMAIN 응답 코드가 반환 됩니다. |
| &lt;일부&gt; |사용 안 함 |사용 안 함 |hello 끝점에 사용할 수 없습니다. 사용하지 않도록 설정된 끝점이 모니터링되지 않습니다. hello 끝점 DNS 응답에 포함 되지 않은, 따라서 트래픽을 수신 하지 않습니다. |
| 사용 |사용 |온라인 |hello 끝점을 모니터링 하 고 정상 상태입니다. DNS 응답에 포함되며 트래픽을 수신할 수 있습니다. |
| 사용 |사용 |성능 저하됨 |끝점 모니터링 상태 검사에 실패했습니다. hello 끝점 DNS 응답에 포함 되지 않은 하 고 트래픽을 받지 않습니다. <br>예외 toothis 이면 모든 끝점이 저하 된 경우는 쿼리에서 모두는 것으로 간주 toobe hello 쿼리 응답에 반환).</br>|
| 사용 |사용 |CheckingEndpoint |hello 끝점 모니터링 되 고 있지만 hello hello 첫 번째 검색 결과가 아직 수신 되지 않았습니다. CheckingEndpoint는 일반적으로 바로 뒤에 추가 하거나 hello 프로필의 끝점을 사용 하도록 설정 하는 임시 상태입니다. 이 상태의 끝점은 DNS 응답에 포함되며 트래픽을 수신할 수 있습니다. |
| 사용 |사용 |중지됨 |hello 클라우드 서비스 또는 웹 응용 프로그램 실행 되 고 있지 끝점 포인트 toois hello입니다. Hello 클라우드 서비스나 웹 응용 프로그램 설정을 확인 합니다. 이 hello 끝점 인지 중첩 된 끝점을 입력 하 고 hello 자식 프로필 사용 되지 않는지 또는 비활성 상태인 경우도 발생할 수 있습니다. <br>Stopped 상태의 끝점은 모니터링되지 않습니다. DNS 응답에 포함되지 않으며 트래픽을 수신하지 않습니다. 예외 toothis 모든 끝점이 저하 된 경우 이러한 모든 값으로 간주 됩니다 toobe hello 쿼리 응답에 반환 됩니다.</br>|

중첩된 끝점의 끝점 모니터 상태가 계산되는 방식에 대한 자세한 내용은 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 참조하세요.

### <a name="profile-monitor-status"></a>프로필 모니터 상태

hello 프로필 모니터 상태는 hello 구성 프로필 상태 및 모든 끝점에 대 한 hello 끝점 모니터 상태 값의 조합입니다. 가능한 값 hello hello 다음 표에 설명 되어 있습니다.

| 프로필 상태(구성된 대로) | 끝점 모니터 상태 | 프로필 모니터 상태 | 참고 사항 |
| --- | --- | --- | --- |
| 사용 안 함 |&lt;일부&gt; 또는 정의된 끝점이 없는 프로필 |사용 안 함 |hello 프로필에 사용할 수 없습니다. |
| 사용 |하나 이상의 끝점의 hello 상태 저하 됩니다. |성능 저하됨 |Hello 개별 끝점 상태 값 toodetermine 끝점 주의가 필요를 검토 합니다. |
| 사용 |하나 이상의 끝점의 hello 상태는 온라인입니다. Degraded 상태의 끝점이 없습니다. |온라인 |hello 서비스가 트래픽을 받아들이고 합니다. 별도의 작업이 필요하지 않습니다. |
| 사용 |hello 하나 이상의 끝점 상태가 CheckingEndpoint 합니다. Online 또는 Degraded 상태인 끝점이 없습니다. |CheckingEndpoints |이러한 전환 상태는 프로필을 만들거나 사용하도록 설정하면 발생합니다. hello 끝점 상태는 검사할 hello에 대 한 처음으로입니다. |
| 사용 |hello 프로필의 모든 끝점의 hello 상태는 Disabled 또는 Stopped, 또는 hello 프로필에 정의 된 끝점이 없습니다. |비활성 |끝점이 활성 상태 이면 있더라도 hello 프로필은 여전히 설정 되어 있습니다. |

## <a name="endpoint-failover-and-recovery"></a>끝점 장애 조치 및 복구

트래픽 관리자는 주기적으로 비정상 끝점을 포함 하 여 모든 끝점의 hello 상태를 확인 합니다. Traffic Manager는 끝점이 정상 상태가 되는지 감지한 후 다시 회전에 포함시킵니다.

Hello 다음 이벤트 중 하나가 발생할 때 끝점 손상 되었습니다.
- 프로토콜을 모니터링 하는 hello HTTP 또는 HTTPS 인 경우
    - 200이 아닌 응답을 받았습니다(다양한 2xx 코드 또는 301/302 리디렉션).
- TCP 프로토콜을 모니터링 하는 hello 경우: 
    - 응답은 ACK 또는 SYN ACK toohello 동기화 요청 응답으로에서 받은 것과 다른 전송 tooattempt 트래픽 관리자에서 연결 설정.
- 시간 초과. 
- 모든 다른 연결 문제가 발생 hello 끝점 연결할 수 없게 합니다.

실패한 검사의 문제 해결에 대한 자세한 내용은 [Azure Traffic Manager의 Degraded 상태 문제 해결](traffic-manager-troubleshooting-degraded.md)을 참조하세요. 

hello 그림 2에는 다음 타임 라인은 hello 설정을 다음을 있는 트래픽 관리자 끝점의 프로세스를 모니터링 하는 hello에 대 한 자세한 설명은: 모니터링 프로토콜은 HTTP, 검색 간격은 30 초, 허용된 실패 횟수는 3 시간 제한 값 10 초 이며 DNS TTL은 30 초입니다.

![Traffic Manager 끝점 장애 조치 및 장애 복구 순서](./media/traffic-manager-monitoring/timeline.png)

**그림 2: Traffic Manager 끝점 장애 조치(failover) 및 복구 순서**

1. **GET**. 각 끝점에 대 한 트래픽 관리자 모니터링 시스템이 hello hello 모니터링 설정에에서 지정 된 hello 경로에 GET 요청을 수행 합니다.
2. **200 OK**. 모니터링 시스템 hello는 10 초 이내에 반환 하는 HTTP 200 OK 메시지가 toobe가 필요 합니다. 이 응답을 받으면 hello 서비스를 사용할 수 있는지를 인식 합니다.
3. **확인 간격 30초**. hello 끝점 상태 검사에는 30 초 마다 반복 됩니다.
4. **서비스를 사용할 수 없음**. hello 서비스 사용할 수 없습니다. 트래픽 관리자 hello 다음 상태 확인 될 때까지 확인할 수 없습니다.
5. **경로 모니터링 하는 시도 tooaccess hello**합니다. hello 모니터링 시스템이 GET 요청을 수행 하지만 10 초 hello 제한 시간 내에서 응답을 수신 하지 않습니다 (또는 200 이외의 응답이 수신 될 수 있습니다). 30초 간격으로 3회 더 시도합니다. 성공한 경우 hello 시도 중 하나가 시도 hello 수 다시 설정 됩니다.
6. **상태가 설정 tooDegraded**합니다. 네 번째 연속 된 실패 후 시스템을 모니터링 하는 hello Degraded로 hello 사용할 수 없는 끝점 상태를 표시 합니다.
7. **전환 된 tooother 끝점 트래픽은**합니다. hello 트래픽 관리자 DNS 이름 서버에 업데이트 되 고 트래픽 관리자는 더 이상 hello 끝점 응답 tooDNS 쿼리에서 반환 합니다. 새 연결은 방향이 지정 된 tooother, 사용 가능한 끝점 됩니다. 그러나 이 끝점을 포함하는 이전 DNS 응답은 재귀 DNS 서버 및 DNS 클라이언트에 의해 계속 캐시될 수 있으므로 클라이언트는 hello DNS 캐시가 만료 될 때까지 toouse hello 끝점을 계속 합니다. Hello DNS 캐시가 만료 되 면으로 클라이언트는 새 DNS 쿼리를 만들고 toodifferent 방향이 지정 된 끝점에는 합니다. hello 캐시 기간 hello 트래픽 관리자 프로필, 예를 들어 30 초에서에서 hello TTL 설정에 의해 제어 됩니다.
8. **계속 상태 검사**. 트래픽 관리자 Degraded 상태 된 동안 hello 끝점의 toocheck hello 상태를 계속 합니다. 트래픽 관리자 끝점 hello toohealth 반환 될 때 검색 합니다.
9. **서비스가 다시 온라인 상태가 됩니다**. hello 서비스를 사용할 수 있습니다. hello 모니터링 시스템에서 다음 상태 검사를 수행할 때까지 hello 끝점에서 트래픽 관리자 Degraded 상태를 유지 합니다.
10. **트래픽 tooservice 재개**합니다. Traffic Manager는 GET 요청을 전송하고 200 OK 상태 응답을 수신합니다. hello 서비스 tooa 정상 상태를 반환 했습니다. 트래픽 관리자 이름 서버 hello 업데이트 되 고 DNS 응답에서 hello 서비스의 DNS 이름을 toohand를 시작 합니다. 트래픽이 다른 끝점을 반환 하는 DNS 응답을 캐시 만료 tooother 끝점이 기존 연결으로 종료 되 고 toohello 끝점을 반환 합니다.

    > [!NOTE]
    > 트래픽 관리자 hello DNS 수준에서 작동 하기 때문에 기존 연결 tooany 끝점 영향을 줄 수 없습니다. (또는 변경 된 프로필 설정을 사용 하 여 장애 복구 또는 장애 조치 하는 동안) 끝점 간의 트래픽, 하도록 지시 하는 경우 트래픽 관리자는 새 연결 tooavailable 끝점을 전달 합니다. 그러나 다른 끝점 해당 세션은 종료 될 때까지 tooreceive 트래픽이 기존 연결을 통해 계속 될 수 있습니다. 기존 연결에서 tooenable 트래픽 toodrain, 응용 프로그램을 제한 해야 hello 이며 각 끝점은 사용 되는 세션 기간.

## <a name="traffic-routing-methods"></a>트래픽 라우팅 방법

끝점 Degraded 상태가 더 이상 응답 tooDNS 쿼리에서 반환 됩니다. 대신 대체 끝점이 선택되어 반환됩니다. hello 트래픽 라우팅을 메서드 hello 프로필에 구성 된 hello 대체 끝점을 선택 하는 방법을 결정 합니다.

* **우선 순위**. 끝점은 우선 순위가 정해진 목록을 구성합니다. hello hello 목록에 첫 번째 사용 가능한 끝점은 항상 반환 됩니다. 끝점 상태 저하 되 면 hello 다음 사용 가능한 끝점 반환 됩니다.
* **가중치 적용**. 모든 사용 가능한 끝점의 할당 된 가중치에 따라 임의로 선택 됩니다 및 hello 가중치 hello의 다른 사용 가능한 끝점입니다.
* **성능**. hello 끝점 가장 가까운 toohello 최종 사용자가 반환 됩니다. 끝점에서 임의로 선택은 해당 끝점에 사용할 수 없는 경우 모든 hello 다른 사용 가능한 끝점입니다. 오버 로드 된 hello 가장 가까운 다음 끝점이 될 때 발생할 수 있는 연속 오류를 방지 임의의 끝점을 선택 합니다. [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region)을 사용하여 성능 트래픽 라우팅에 대한 대체 장애 조치 계획을 구성할 수 있습니다.
* **지리적**. hello 끝점 IP가 반환 되는 hello 쿼리 요청에 따라 tooserve hello 지리적 위치가 매핑됩니다. 해당 끝점에 사용할 수 없는 경우 다른 끝점 됩니다, 선택한 toofailover 지리적 위치 프로필에 매핑된 전용 tooone 끝점 될 수 있으므로 (자세한 세부 정보는 hello에서 [FAQ](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). 모범 사례로, 지리적 라우팅을 사용 하는 경우, 권장 여러 끝점을 사용 하 여 toouse 중첩 된 트래픽 관리자 프로필 hello 프로필의 hello 끝점으로 합니다.

자세한 내용은 [트래픽 관리자 트래픽 라우팅 방법](traffic-manager-routing-methods.md)을 참조하세요.

> [!NOTE]
> 행동 한 가지 예외 toonormal 트래픽 라우팅을 모든 적격 끝점 성능이 저하 된 상태에 있을 때 발생 합니다. 트래픽 관리자는 한 "최상의" 시도 및 *온라인 상태에서 모든 hello Degraded 상태 끝점이 실제로 처럼 응답*합니다. 이 동작은 만드는 것이 좋습니다 toohello 대신 toonot hello DNS 응답의에서 모든 끝점을 반환 합니다. Disabled 또는 Stopped 끝점은 모니터링되지 않으므로 트래픽에 적합한 것으로 간주되지 않습니다.
>
> 이 문제는 일반적으로 같은으로 인해 발생 hello 서비스의 잘못 된 구성:
>
> * 액세스 제어 목록 [ACL] hello 트래픽 관리자 상태 검사를 차단 합니다.
> * Hello 트래픽 관리자 프로필에서에서 프로토콜 또는 포트를 모니터링 하는 hello의 부적절 한 구성입니다.
>
> hello이 동작의 결과 트래픽 관리자 상태 검사 올바르게 구성 되지 않은 경우 hello 트래픽 트래픽 관리자 라우팅 것 처럼 나타날 수 있습니다 것 *은* 정상적으로 작동 합니다. 하지만 이 경우에 전체 응용 프로그램 가용성에 영향을 미치는 끝점 장애 조치는 발생할 수 없습니다. 것이 중요 한 toocheck hello 프로필에는 온라인 상태를 저하 됨 상태 하지 표시 되는지 합니다. 온라인 상태는 해당 hello 상태 검사 예상 대로 작동 하는 트래픽 관리자를 나타냅니다.

실패한 상태 검사의 문제 해결에 대한 자세한 내용은 [Azure Traffic Manager의 Degraded 상태 문제 해결](traffic-manager-troubleshooting-degraded.md)을 참조하세요.



## <a name="next-steps"></a>다음 단계

[Traffic Manager 작동 방식](traffic-manager-how-traffic-manager-works.md)

Hello에 대 한 자세한 [트래픽 라우팅 방법](traffic-manager-routing-methods.md) 트래픽 관리자에서 지원

너무 방법에 대해 알아봅니다[트래픽 관리자 프로필 만들기](traffic-manager-manage-profiles.md)

[Degraded 상태 문제를 해결](traffic-manager-troubleshooting-degraded.md) 합니다.

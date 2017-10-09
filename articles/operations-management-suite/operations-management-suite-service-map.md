---
title: "aaaUse hello Operations Management Suite에서 서비스 맵을 솔루션 | Microsoft Docs"
description: "서비스 맵을 Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 Operations Management Suite 솔루션 및 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다. 이 문서에서는 사용자 환경에 서비스 맵을 배포하고 다양한 시나리오에서 사용하는 것에 대해 자세히 설명합니다."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Hello 서비스 맵 솔루션을 사용 하 여 Operations Management Suite에서
Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색 하는 서비스 지도 및 지도 hello 서비스 간의 통신 합니다. 서비스 맵을 사용 하 여 hello 방법으로 서버를 볼 수 있습니다: 중요 한 서비스를 제공 하는 상호 연결 된 시스템으로 합니다. 서비스 맵을 TCP 연결 하는 모든 아키텍처에서 서버, 프로세스 및 포트 간의 연결을 표시, hello 에이전트 설치와 구성이 아닌 다른 필요 하지 않습니다.

이 문서에서는 서비스 맵을 사용 하 여의 hello 세부 정보를 설명 합니다. 서비스 맵 구성 및 에이전트 탑재에 대한 정보는 [Operations Management Suite에서 서비스 맵 솔루션 구성](operations-management-suite-service-map-configure.md)을 참조하세요.


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>사용 사례: IT 프로세스 종속성 인식

### <a name="discovery"></a>검색
서비스 맵은 서버, 프로세스 및 타사 서비스 간 종속성에 대한 일반적인 참조 맵을 자동으로 작성합니다. 검색 하 고 예기치 않은 연결, 원격 제 3 자 시스템에서 사용 및 Active Directory와 같은 네트워크의 종속성 tootraditional 어두운 영역을 식별 하는 모든 TCP 종속성을 매핑합니다. 서비스 맵을 잠재적인 서버 잘못 된 구성, 서비스 중단 및 네트워크 문제를 식별 하는 데 도움이 관리 시스템, toomake를 시도 하는 실패 한 네트워크 연결을 검색 합니다.

### <a name="incident-management"></a>인시던트 관리
서비스 맵을 시스템 연결 되는 방법을 보여 주는 및 서로 영향을 주는 문제 격리의 hello 추측을 제거할 수 있습니다. 또한 tooidentifying 실패 연결, 잘못 구성 된 부하 분산 장치, 중요 한 서비스에 놀라운 또는 과도 한 부하를 식별 하 고 악의적인 tooproduction 시스템 통하게 개발자 컴퓨터 등의 클라이언트는 데 도움이 됩니다. Operations Management Suite 변경 내용 추적을 통합 된 워크플로 이용해 인시던트의 hello 근본 원인을 백 엔드 시스템 또는 서비스에서 변경 이벤트에 설명 하는지 여부를 확인할 수 있습니다.

### <a name="migration-assurance"></a>마이그레이션 보증
서비스 맵을 사용하면, Azure Migration을 효과적으로 계획, 가속화 및 검증할 수 있으므로 아무것도 남기지 않고 임의의 중단이 발생하지 않도록 할 수 있습니다. 모든 상호 종속 된 시스템 해당 필요 toomigrate 함께 검색 하 고, 시스템 구성 및 용량을 평가 하 고, 실행 중인 시스템 여전히 제공 하는 중인 사용자 또는 마이그레이션 대신 서비스 해제에 대 한 대상 인지 여부를 확인할 수입니다. Hello 이동이 완료 한 후 시스템을 테스트 하는 클라이언트 부하 및 id tooverify에서 확인할 수 있습니다 및 고객을 연결 하는 합니다. 서브넷 계획 및 방화벽 정의 문제가 서비스 맵을 맵에서 실패 한 연결 지점 수는 연결 해야 하는 toohello 시스템을 사용 합니다.

### <a name="business-continuity"></a>비즈니스 연속성
Azure Site Recovery를 사용 하는 해야 서비스 맵 환경에 응용 프로그램에 대 한 hello 복구 시퀀스를 정의 하는 도움말 수 자동으로 표시 하면 어떻게 시스템에 의존 서로 tooensure 복구 계획은 신뢰할 수 있는 합니다. Hello 서버 복원 되어 사용 가능한 후 중요 한 서버 또는 그룹을 선택 하 고 해당 클라이언트 보기를 여는 프런트 엔드 시스템 toorecover를 식별할 수 있습니다. 반대로, 중요 한 서버의 백 엔드 종속성을 보고 식별할 수 있습니다는 시스템 toorecover 포커스 시스템을 복원 하기 전에.

### <a name="patch-management"></a>패치 관리
서비스 맵을 다른 팀과 서버에 따라 결정 되 사용자가 서비스를 패치 기능에 시스템 수행 하기 전에 사전에 알릴 수 있습니다 하므로 표시 하 여 hello Operations Management Suite 시스템 업데이트 평가의 사용을 향상 시킵니다. 서비스 맵은 또한 패치되고 다시 시작된 후 서비스가 사용 가능하고 올바르게 연결되었는지를 보여줌으로써 Operations Management Suite의 패치 관리를 향상시킵니다.


## <a name="mapping-overview"></a>매핑 개요
서비스 맵을 에이전트 hello 설치 하 고 서버에서 세부 정보에 대 한 hello 각 프로세스에 대 한 인바운드 및 아웃 바운드 연결에 TCP 연결의 모든 프로세스에 대 한 정보를 수집 합니다. Hello 왼쪽된 창에서 hello 목록에서 컴퓨터 또는 지정 된 시간 범위 동안 서비스 맵을 에이전트 toovisualize 해당 종속성이 있는 그룹을 선택할 수 있습니다. 컴퓨터 종속성 특정 컴퓨터에 초점을 매핑하고 직접 TCP 클라이언트 또는 서버 해당 컴퓨터의 모든 hello 컴퓨터를 표시 합니다.  컴퓨터 그룹 맵은 일련의 서버 및 서버 종속성을 보여줍니다.

![서비스 맵 개요](media/oms-service-map/service-map-overview.png)

Hello 선택한 시간 범위 동안 활성 네트워크 연결을 통해 프로세스를 실행 하는 hello 맵 tooshow hello에 컴퓨터를 확장할 수 있습니다. 서비스 맵 에이전트와 원격 컴퓨터가 확장된 tooshow 프로세스 정보 이면 hello 포커스 컴퓨터와 통신 하는 프로세스에만 표시 됩니다. hello hello 포커스 컴퓨터에 연결 하는 에이전트 없는 프런트 엔드 컴퓨터 수는 hello hello 프로세스에 연결 되지 않은 왼쪽된에 표시 됩니다. Hello 포커스 컴퓨터에 에이전트가 없습니다. 연결 tooa 백 엔드 시스템을 하는 hello 백 엔드 서버가 서버 포트 그룹에 포함 되어, 다른 연결 toohello 함께 동일한 포트 번호입니다.

기본적으로 서비스 맵을 표시 hello를 마지막 30 분의 종속성 정보를 매핑합니다. 왼쪽 위에서 hello에 hello 타임 컨트롤을 사용해를 tooone 시간 tooshow hello에 종속성을 조회 하는 방법을 기록 시간 범위에 대 한 맵을 쿼리할 수 있습니다 (예: 인시던트 동안 또는 변경이 발생 하기 전에) 과거입니다. 서비스 맵 데이터는 유료 작업 영역에서 30일 동안, 무료 작업 영역에서는 7일 동안 저장됩니다.

## <a name="status-badges-and-border-coloring"></a>상태 배지 및 경계 색 지정
Hello에 hello 지도 있는 각 서버의 아래쪽 hello 서버에 대 한 상태 정보를 전달 하는 상태 배지 목록이 될 수 있습니다. hello 배지 hello Operations Management Suite 솔루션 통합 중 하나에서 서버 hello에 대 한 관련 정보가 있음을 나타냅니다. 클릭는 배지 이동할 직접 hello 상태의 toohello 세부 정보 hello 오른쪽 창에 있습니다. hello 현재 사용 가능한 상태 배지 포함 경고 "," 서비스 창구 "," 변경 "," 보안 "및" 업데이트 됩니다.

Hello 상태 배지의 hello 심각도 따라 컴퓨터 노드 테두리 색이 지정 된 빨강 (위험), 노랑 (경고) 하거나 파란색 (정보) 수 있습니다. hello 색 hello 상태 배지의 hello 가장 심각한 상태를 나타냅니다. 회색 테두리는 상태 표시기가 없는 노드를 나타냅니다.

![상태 배지](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>컴퓨터 그룹
컴퓨터 그룹을 사용 하면 toosee 지도 뿐 아니라 하나 이상의 매핑이 두 개에 있는 다층 계층 응용 프로그램 또는 서버 클러스터의 모든 hello 멤버를 볼 수 있도록 서버 집합을 중심으로 합니다.

사용자가 선택한 서버를 함께 그룹에 속하는 hello 그룹에 대 한 이름을 선택 합니다.  그런 다음 모든 프로세스와 연결을 사용 하 여 tooview hello 그룹을 선택 하거나 hello 그룹의 다른 구성원과 hello 프로세스 및 toohello 직접 관련 된 연결 사용 하 여 볼 수 있습니다.

![컴퓨터 그룹](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>컴퓨터 그룹 만들기
hello 컴퓨터에 나열 하 고 클릭 하 여 원하는 그룹 toocreate, 선택 hello 컴퓨터 또는 컴퓨터 **toogroup 추가**합니다.

![그룹 만들기](media/oms-service-map/machine-groups-create.png)

선택할 수 있습니다 **새로 만들기** hello 그룹 이름을 지정 합니다.

![그룹 이름 지정](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>컴퓨터 그룹은 현재 제한 too10 서버 하지만 계획 tooincrease이 한이도 곧 합니다.

### <a name="viewing-a-group"></a>그룹 보기
일부 그룹을 만든 후에 hello 그룹 탭을 선택 하 여 볼 수 있습니다.

![그룹 탭](media/oms-service-map/machine-groups-tab.png)

해당 컴퓨터 그룹에 대 한 hello 그룹 이름 tooview hello 맵을 선택 합니다.
![컴퓨터 그룹](media/oms-service-map/machine-group.png) toohello 그룹에 속하는 hello 컴퓨터 hello 맵에서 흰색에 설명 되어 있습니다.

그룹 확장 hello hello 컴퓨터 그룹을 구성 하는 hello 컴퓨터를 나열 합니다.

![컴퓨터 그룹 컴퓨터](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>프로세스별 필터링
Hello 그룹의에서 모든 프로세스 및 연결 표시 간 hello 맵 보기를 설정/해제할 수 있으며만 직접 toohello 컴퓨터 그룹을 연결 하는 스토리를 hello 수 있습니다.  기본 보기 hello tooshow 모든 프로세스는 합니다.  Hello 맵 위에 hello 필터 아이콘을 클릭 하 여 hello 보기를 변경할 수 있습니다.

![필터 그룹](media/oms-service-map/machine-groups-filter.png)

때 **모든 프로세스** 은 선택 하면 hello 지도에 포함 됩니다는 모든 프로세스와 각각의 hello 컴퓨터에서 연결 hello 그룹입니다.

![컴퓨터 그룹 모든 프로세스](media/oms-service-map/machine-groups-all.png)

Hello 보기 tooshow만 변경 하는 경우 **그룹에 연결 된 프로세스**, hello 맵 좁혀 질 프로세스 및 연결을 직접 연결 hello 그룹, 간단한 보기를 만드는 방법의 tooother 컴퓨터 tooonly 다운 합니다.

![컴퓨터 그룹 필터링된 프로세스](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>추가 컴퓨터 tooa 그룹
tooadd tooan 기존 그룹 컴퓨터, hello 상자를 선택한 다음 다음 toohello 컴퓨터 확인 **toogroup 추가**합니다.  그런 다음 hello 그룹 tooadd hello 컴퓨터를 선택 합니다.
 
### <a name="removing-machines-from-a-group"></a>컴퓨터를 그룹에서 제거
Hello 그룹 목록, hello 컴퓨터 그룹의에서 hello 그룹 이름 toolist hello 컴퓨터를 확장 합니다.  그런 다음 컴퓨터를 클릭 hello 줄임표 메뉴 다음 toohello tooremove를 원하고 선택 **제거**합니다.

![컴퓨터를 그룹에서 제거](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>그룹 제거 또는 이름 변경
Hello 줄임표 메뉴 다음 toohello에에서 그룹 이름을 hello 그룹 목록에서 클릭 합니다.

![컴퓨터 그룹 메뉴](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>역할 아이콘
특정 프로세스는 컴퓨터에서 웹 서버, 응용 프로그램 서버, 데이터베이스 등과 같은 특정 역할을 담당합니다. 서비스 맵을 프로세스 주석을 달고 재생 눈 hello 역할 프로세스 또는 서버 역할 아이콘 toohelp으로 컴퓨터 상자 식별 합니다.

| 역할 아이콘 | 설명 |
|:--|:--|
| ![웹 서버](media/oms-service-map/role-web-server.png) | 웹 서버 |
| ![앱 서버](media/oms-service-map/role-application-server.png) | 응용 프로그램 서버 |
| ![데이터베이스 서버](media/oms-service-map/role-database.png) | 데이터베이스 서버 |
| ![LDAP 서버](media/oms-service-map/role-ldap.png) | LDAP 서버 |
| ![SMB 서버](media/oms-service-map/role-smb.png) | SMB 서버 |

![역할 아이콘](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>실패한 연결
실패 한 연결에 표시 된 서비스 맵을 사용 프로세스 및 컴퓨터에 대 한 클라이언트 시스템 tooreach 실패를 나타내는 빨간색 파선으로 프로세스 또는 포트입니다. 실패 한 연결 해당 시스템 hello 하나의 하려고 하는 동안 실패 hello 연결 인 경우 배포 된 서비스 맵을 에이전트와 함께 모든 시스템에서 보고 됩니다. 서비스 맵을 tooestablish 실패 하는 TCP 소켓 연결을 관찰 하 여이 프로세스를 측정 합니다. 방화벽을 hello 클라이언트 또는 서버에서 잘못 된 구성에서이 오류가 발생할 수 또는 원격 서비스를 사용할 수 없게 합니다.

![실패한 연결](media/oms-service-map/failed-connections.png)

실패한 연결을 이해하면 문제 해결, 마이그레이션 유효성 검사, 보안 분석 및 전체 아키텍처를 이해하는 데 도움이 됩니다. 실패 한 연결 무해 경우도 있지만 종종 가리키는지 직접 갑자기 연결할 수 없는 경우 되 고 장애 조치 환경 또는 두 개의 응용 프로그램 계층 클라우드 마이그레이션 후 없습니다 tootalk 되 고 같은 tooa 문제.

## <a name="client-groups"></a>클라이언트 그룹
클라이언트 그룹은 종속성 에이전트를 갖지 않는 클라이언트 컴퓨터를 나타내는 hello 지도에 상자입니다. 단일 클라이언트 그룹에는 개별 프로세스 또는 컴퓨터에 대 한 hello 클라이언트를 나타냅니다.

![클라이언트 그룹](media/oms-service-map/client-groups.png)

클라이언트 그룹을 선택 hello 그룹 hello 서버 toosee hello IP 주소입니다. hello 그룹의 hello 내용을 hello에 나열 됩니다 **클라이언트 그룹 속성** 창.

![클라이언트 그룹 속성](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>서버 포트 그룹
서버 그룹은 종속성 에이전트가 없는 서버의 서버 포트를 나타내는 상자입니다. hello 상자 hello 서버 포트 및 연결 toothat 포트와 서버 hello 수의 수가 포함 됩니다. Hello 상자 toosee hello 개별 서버와 연결을 확장 합니다. Hello 상자에 서버를 하나만 있으면 hello 이름이 나 IP 주소가 나열 됩니다.

![서버 포트 그룹](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>상황에 맞는 메뉴
Hello 위쪽에 hello 줄임표 (...)를 클릭 하면 오른쪽 모든 서버에 해당 서버에 대 한 hello 상황에 맞는 메뉴를 표시 합니다.

![실패한 연결](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>서버 맵 로드
클릭 하면 **서버 맵 로드** tooa 새 맵을 hello 새 포커스 컴퓨터 서버에 선택한 hello로 이동 합니다.

### <a name="show-self-links"></a>자체 링크 표시
클릭 하면 **표시 Self-Links** 다시 그리기 횟수 hello 서버 노드를 포함 하 여 자체 링크를 시작 하 고 hello 서버 내에서 프로세스를 종료 하는 TCP 연결이 설정 되어 있는 합니다. 경우 자체 링크는 표시, 너무 메뉴 명령 변경 내용은 hello**숨기기 Self-Links**를 하 여 설정할 수 있습니다.

## <a name="computer-summary"></a>컴퓨터 요약
hello **컴퓨터 요약** 창 서버의 운영 체제, 종속성 개수 및 다른 Operations Management Suite 솔루션의에서 데이터에 대 한 개요를 포함 합니다. 이러한 데이터에는 성능 메트릭, 서비스 데스크 티켓, 변경 내용 추적, 보안 및 업데이트가 포함됩니다.

![컴퓨터 요약 창](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>컴퓨터 및 프로세스 속성
서비스 맵 지도 표시할 경우 해당 속성에 대 한 컴퓨터 및 프로세스 toogain 추가 컨텍스트를 선택할 수 있습니다. 컴퓨터는 DNS 이름, IPv4 주소, CPU 및 메모리 용량, VM 유형, 운영 체제 및 버전, 마지막 부팅 시간 및 해당 서비스 맵 및 Operations Management Suite 에이전트의 hello Id에 대 한 정보를 제공 합니다.

![컴퓨터 속성 창](media/oms-service-map/machine-properties.png)

운영 체제 메타데이터에서 프로세스 이름, 프로세스 설명, 사용자 이름 및 도메인(Windows), 회사 이름, 제품 이름, 제품 버전, 작업 디렉터리, 명령줄 및 프로세스 시작 시간을 비롯한 실행 중인 프로세스에 대한 프로세스 정보를 수집할 수 있습니다.

![프로세스 속성 창](media/oms-service-map/process-properties.png)

hello **프로세스 요약** 창 해당 바인딩된 포트, 인바운드 및 아웃 바운드 연결을 포함 하 여 hello 프로세스의 연결에 대 한 추가 정보를 제공 하 고 연결 하지 못했습니다.

![프로세스 요약 창](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Operations Management Suite 경고 통합
서비스 맵을 hello 선택한 시간 범위에서 선택한 서버 hello에 대 한 Operations Management Suite 경고 발생 tooshow 경고와 통합 됩니다. 현재 경고가 hello 서버 아이콘을 표시 하 고 hello **컴퓨터 경고** 창 hello 알림을 표시 합니다.

![컴퓨터 경고 창](media/oms-service-map/machine-alerts.png)

tooenable 서비스 맵을 toodisplay 관련 경고를 특정 컴퓨터에 대해 발생 하는 경고 규칙을 만듭니다. toocreate 적절 한 알림:
- 컴퓨터별 절 toogroup 포함 (예를 들어 **컴퓨터 1 분 간격으로**).
- Tooalert 메트릭 측정에 기반을 선택 합니다.

![경고 구성](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Operations Management Suite 로그 이벤트 통합
서비스 맵을 통합 로그 검색 tooshow hello 선택한 서버에 대 한 모든 사용 가능한 로그 이벤트의 개수 hello 선택한 시간 범위 동안 합니다. 이벤트 개수 toojump tooLog 검색의 hello 목록에서 임의의 행을 클릭 하 고 hello 개별 로그 이벤트를 확인할 수 있습니다.

![컴퓨터 로그 이벤트 창](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Operations Management Suite 서비스 데스크 통합
서비스 맵 통합 IT 서비스 관리 커넥터 hello로 이러한 솔루션 둘 다 사용 하도록 설정 되 고 Operations Management Suite 작업 영역에서 구성 하는 경우 자동 수행 됩니다. 서비스 맵에서 hello 통합 레이블이 "서비스 창구"입니다. 자세한 내용은 [IT Service Management Connector를 사용하여 ITSM 작업 항목을 중앙에서 관리](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview)를 참조하세요.

hello **컴퓨터 서비스 데스크** 창 hello 선택한 시간 범위에서 선택한 서버 hello에 대 한 모든 IT 서비스 관리 이벤트를 나열 합니다. 현재 항목을 hello 컴퓨터 서비스 데스크 창 나열 하면 hello 서버 아이콘을 표시 합니다.

![컴퓨터 서비스 데스크 창](media/oms-service-map/service-desk.png)

연결 된 ITSM 솔루션에서는 tooopen hello 항목 클릭 **작업 항목 보기**합니다.

로그 검색에 hello 항목의 tooview hello 세부 정보 클릭 **로그 검색에 표시**합니다.


## <a name="operations-management-suite-change-tracking-integration"></a>Operations Management Suite 변경 내용 추적 통합
변경 내용 추적과 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정화하고 구성하면 자동으로 수행됩니다.

hello **시스템 변경 내용 추적** 창에서는 가장 최근의 hello로 모든 변경 내용을 먼저 tooLog 추가 세부 정보에 대 한 검색 다운 링크 toodrill 함께 합니다.

![컴퓨터 변경 내용 추적 창](media/oms-service-map/change-tracking.png)

hello 다음 이미지는 표시 될 수 있는 ConfigurationChange 이벤트의 세부 정보 보기를 선택한 후 **로그 분석에 표시할**합니다.

![ConfigurationChange 이벤트](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Operations Management Suite 성능 통합
hello **컴퓨터 성능** 창에 선택한 서버 hello에 대 한 표준 성능 메트릭을 표시 됩니다. hello 메트릭에 네트워크 바이트를 송수신 하 여 CPU 사용률, 메모리 사용률, 네트워크 바이트, 전송 및 수신 및 hello 상위 프로세스 목록을 포함 합니다. tooget hello 네트워크 성능 데이터도 설정 해야 hello Operations Management Suite에 실시간 데이터 2.0 솔루션입니다.

![컴퓨터 성능 창](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Operations Management Suite 보안 통합
보안 및 감사과 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정하고 구성하면 자동으로 수행됩니다.

hello **컴퓨터 보안** 창 hello hello 선택한 서버에 대 한 Operations Management Suite 보안 및 감사 솔루션의에서 데이터를 표시 합니다. hello 창 hello 선택한 시간 범위 동안 서버 hello에 대 한 보안 문제에 대 한 요약을 나열합니다. 다운에 대 한 자세한 내용은 로그 검색으로 hello 보안 문제 드릴 중 하나를 클릭합니다.

![컴퓨터 보안 창](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Operations Management Suite 업데이트 통합
업데이트 관리와 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정화하고 구성하면 자동으로 수행됩니다.

hello **컴퓨터 업데이트** hello hello 선택한 서버에 대 한 Operations Management Suite 업데이트 관리 솔루션에서에서 데이터 창에 표시 됩니다. hello 창 hello 선택한 시간 범위 동안 서버 hello에 대 한 누락 된 업데이트에 대 한 요약을 나열합니다.

![컴퓨터 변경 내용 추적 창](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Log Analytics 레코드
서비스 맵 컴퓨터 및 프로세스 인벤토리 데이터는 Log Analytics에서 [검색](../log-analytics/log-analytics-log-searches.md)할 수 있습니다. 마이그레이션 계획, 용량 분석, 검색 및 요청 시 성능 문제 해결을 포함 하는이 데이터 tooscenarios를 적용할 수 있습니다.

각 고유 컴퓨터와 프로세스에 대 한 시간당 하나의 레코드가 생성 됩니다, 그리고 프로세스 또는 컴퓨터를 시작 하거나 등록 된 tooService은 때 생성 되는 toohello 레코드가 또한 매핑되는지 확인 합니다. 이러한 레코드는 다음 표는 hello에 hello 속성이 있습니다. hello 필드와 hello ServiceMapComputer_CL 이벤트에 대 한 값의 hello hello ServiceMap Azure 리소스 관리자 API의에서 컴퓨터 리소스 toofields를 매핑합니다. hello 필드 및 값 hello ServiceMapProcess_CL 이벤트에서 toohello 필드 매핑 hello hello ServiceMap Azure 리소스 관리자 API에에서 대 한 프로세스 리소스의 합니다. hello ResourceName_s 필드가 hello 이름 필드 hello 해당 하는 리소스 관리자 리소스에 일치합니다. 

>[!NOTE]
>서비스 맵 기능 성장 함에 따라 이러한 필드는 제목 toochange 합니다.

내부적으로 생성 된 속성 tooidentify 고유 프로세스 및 컴퓨터를 사용할 수 있습니다.

- 컴퓨터의 경우: 사용 하 여 ResourceId 또는 ResourceName_s toouniquely를 Operations Management Suite 작업 영역 내에서 컴퓨터를 식별 합니다.
- 프로세스: 사용 하 여 ResourceId toouniquely를 Operations Management Suite 작업 영역 내에서 프로세스를 식별 합니다. ResourceName_s는 hello 컴퓨터는 hello에 프로세스가 실행 되 고 (MachineResourceName_s)의 hello 컨텍스트 내에서 고유 

쿼리 hello에 대 한 레코드가 여러 개를 반환할 수 있으므로 지정된 된 시간 범위에서 컴퓨터와 지정 된 프로세스에 대 한 레코드가 여러 개 존재할 수 있으며, 동일한 컴퓨터 또는 프로세스입니다. tooinclude 최신 레코드를만 hello 추가 "| 중복 제거 ResourceId"toohello 쿼리입니다.

### <a name="servicemapcomputercl-records"></a>ServiceMapComputer_CL 레코드
*ServiceMapComputer_CL* 형식의 레코드는 서비스 맵 에이전트가 있는 서버에 대한 인벤토리 데이터를 포함합니다. 이러한 레코드는 다음 표에 hello에 hello 속성을 포함 합니다.

| 속성 | 설명 |
|:--|:--|
| 형식 | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | hello hello 작업 영역 내에서 컴퓨터에 대 한 고유 식별자 |
| ResourceName_s | hello hello 작업 영역 내에서 컴퓨터에 대 한 고유 식별자 |
| ComputerName_s | hello 컴퓨터의 FQDN |
| Ipv4Addresses_s | Hello 서버의 IPv4 주소 목록이 |
| Ipv6Addresses_s | 목록은 한 hello 서버 IPv6 주소 |
| DnsNames_s | DNS 이름 배열 |
| OperatingSystemFamily_s | Windows 또는 Linux |
| OperatingSystemFullName_s | hello hello 운영 체제의 전체 이름  |
| Bitness_s | hello 컴퓨터 (32 비트 또는 64 비트)의 hello 비트  |
| PhysicalMemory_d | hello 실제 메모리 (MB) |
| Cpus_d | hello Cpu 수 |
| CPUSpeed_d | hello mhz에서 CPU 속도|
| VirtualizationState_s | *unknown*, *physical*, *virtual*, *hypervisor* |
| VirtualMachineType_s | *hyperv*, *vmware* 등 |
| VirtualMachineNativeMachineId_g | hello VM ID는 하이퍼바이저에서 할당 |
| VirtualMachineName_s | hello VM의 hello 이름 |
| BootTime_t | hello 부팅 시간 |



### <a name="servicemapprocesscl-type-records"></a>ServiceMapProcess_CL 형식 레코드
*ServiceMapProcess_CL* 형식의 레코드는 서비스 맵 에이전트가 있는 서버에서 TCP 연결 프로세스에 대한 인벤토리 데이터를 포함합니다. 이러한 레코드는 다음 표에 hello에 hello 속성을 포함 합니다.

| 속성 | 설명 |
|:--|:--|
| 형식 | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | hello hello 작업 영역 내에서 프로세스에 대 한 고유 식별자 |
| ResourceName_s | hello 실행 되는 hello 컴퓨터 내에서 프로세스에 대 한 고유 식별자|
| MachineResourceName_s | hello 컴퓨터의 hello 리소스 이름 |
| ExecutableName_s | hello 프로세스 실행 파일의 hello 이름 |
| StartTime_t | hello 프로세스 풀 시작 시간 |
| FirstPid_d | hello hello 프로세스 풀에서 첫 번째 PID |
| Description_s | hello 프로세스 설명 |
| CompanyName_s | hello 회사의 hello 이름 |
| InternalName_s | hello 내부 이름 |
| ProductName_s | hello hello 제품 이름 |
| ProductVersion_s | hello 제품 버전 |
| FileVersion_s | hello 파일 버전 |
| CommandLine_s | hello 명령줄 |
| ExecutablePath _s | hello 경로 toohello 실행 파일 |
| WorkingDirectory_s | hello 작업 디렉터리 |
| 사용자 이름 | 프로세스가 실행 되는 hello hello 계정 |
| UserDomain | 프로세스가 실행 되는 hello hello 도메인 |


## <a name="sample-log-searches"></a>샘플 로그 검색

### <a name="list-all-known-machines"></a>알려진 모든 컴퓨터 나열
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>모든 관리 컴퓨터의 실제 메모리 용량이 hello를 나열 합니다.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>컴퓨터 이름, DNS, IP 및 OS를 나열합니다.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Hello 명령줄에서 "sql"로 모든 프로세스 찾기
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>리소스 이름으로 컴퓨터(가장 최근 레코드) 찾기
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>IP 주소로 컴퓨터(가장 최근 레코드) 찾기
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>특정 컴퓨터의 알려진 프로세스 모두 나열
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>SQL을 실행하는 모든 컴퓨터를 나열합니다.
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>내 데이터 센터에서 curl의 고유한 제품 버전 모두 나열
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>CentOS를 실행하는 모든 컴퓨터의 컴퓨터 그룹 만들기
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>REST API
서비스 맵을의 모든 hello 서버, 프로세스 및 종속성 데이터는 hello를 통해 사용할 수 있는 [서비스 맵 REST API](https://docs.microsoft.com/rest/api/servicemap/)합니다.


## <a name="diagnostic-and-usage-data"></a>진단 및 사용 현황 데이터
Microsoft는 자동으로 사용 하 여 사용자 hello 서비스 맵 서비스 사용 및 성능 데이터를 수집합니다. Microsoft는이 데이터 tooprovide를 사용 하 여 및 hello 품질, 보안 및 hello 서비스 맵 서비스의 무결성을 향상 합니다. 정확 하 고 효율적인 문제 해결 기능 tooprovide hello 데이터는 운영 체제 및 버전, IP 주소, DNS 이름 및 워크스테이션 이름 같은 소프트웨어의 hello 구성에 대 한 정보를 포함 합니다. 이름, 주소 또는 기타 연락처 정보는 수집하지 않습니다.

데이터 수집 및 사용에 대 한 자세한 내용은 참조 hello [Microsoft 온라인 서비스 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=512132)합니다.


## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [검색 로그](../log-analytics/log-analytics-log-searches.md) 에서 서비스 맵을 통해 수집 되는 로그 분석 tooretrieve 데이터입니다.


## <a name="troubleshooting"></a>문제 해결
Hello 참조 [hello 서비스 맵을 구성 문서의 섹션 문제 해결](operations-management-suite-service-map-configure.md#troubleshooting)합니다.


## <a name="feedback"></a>사용자 의견
서비스 맵 또는 이 설명서에 대한 의견이 있습니까?  기능을 제안하거나 기존 제안에 투표할 수 있는 [사용자 의견 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)를 방문하세요.

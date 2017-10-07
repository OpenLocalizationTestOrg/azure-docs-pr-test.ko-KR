---
title: "OMS의 솔루션 상태 aaaAgent | Microsoft Docs"
description: "이 문서는 어떻게 toouse이 솔루션 toomonitor hello의 상태를 이해 하는 의도 된 toohelp 보고 직접 tooOMS 또는 System Center Operations Manager 에이전트입니다."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>OMS의 에이전트 상태 솔루션
OMS에서 에이전트 상태 솔루션 hello는 모든 있는 응답 하지 않는 및 제출 하는 중 운영 데이터 보고 직접 toohello OMS 작업 영역 또는 System Center Operations Manager 관리 그룹 연결 tooOMS hello 에이전트에 대 한 이해 하도록 도와 줍니다.  또한 유지의 추적 수 있습니다 수 에이전트 배포와, 지리적으로 분산 되어 Azure, 다른 클라우드 환경에서 또는 온-프레미스에 배포 된 에이전트의 hello 분포에 대 한 다른 쿼리 toomaintain 인식을 수행 합니다.    

## <a name="prerequisites"></a>필수 조건
이 솔루션을 배포 하기 전에 확인 현재 지 원하는 [Windows 에이전트](../log-analytics/log-analytics-windows-agents.md) toohello OMS 작업 영역을 보고 하거나 보고 tooan [Operations Manager 관리 그룹](../log-analytics/log-analytics-om-agents.md) 환경과 통합 되어 있으며 사용자 OMS 작업 영역입니다.    

## <a name="solution-components"></a>솔루션 구성 요소
이 솔루션의 hello tooyour 작업 영역 및 직접 연결 된 에이전트 또는 Operations Manager 연결 된 관리 그룹에 추가 되는 리소스를 다음으로 구성 됩니다.

### <a name="management-packs"></a>관리 팩
System Center Operations Manager 관리 그룹에 연결 된 tooan OMS 작업 영역 이면 hello 다음 관리 팩은 Operations Manager에 설치 됩니다.  이 솔루션을 추가한 후 직접 연결된 Windows 컴퓨터에 이러한 관리 팩도 함께 설치됩니다. 더 할 게 없습니다 tooconfigure 또는 이러한 관리 팩을 사용 하 여 관리 합니다.

* Microsoft System Center Advisor 상태 평가 직접 채널 인텔리전스 팩(Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor 상태 평가 서버 채널 인텔리전스 팩(Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

솔루션 관리 팩 업데이트 되는 방식에 대 한 자세한 내용은 참조 하십시오. [Operations Manager 연결 tooLog 분석](../log-analytics/log-analytics-om-agents.md)합니다.

## <a name="configuration"></a>구성
Hello 프로세스를 사용 하 여 OMS 작업 영역에서 설명 하는 hello 에이전트 상태 솔루션 tooyour 추가 [솔루션 추가](../log-analytics/log-analytics-add-solutions.md)합니다. 추가 구성은 필요 없습니다.


## <a name="data-collection"></a>데이터 수집
### <a name="supported-agents"></a>지원되는 에이전트
다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| Windows 에이전트 | 예 | 하트비트 이벤트는 Windows 에이전트에서 직접 수집됩니다.|
| System Center Operations Manager 관리 그룹 | 예 | 하트 비트 이벤트 60 초 마다 toohello 관리 그룹을 보고 하는 에이전트에서 수집 되 고 그런 다음 tooLog 분석을 전달 합니다. Operations Manager 에이전트 tooLog의 직접 연결 분석 필요 하지 않습니다. 하트 비트 이벤트 데이터는 hello 관리 그룹 toohello 로그 분석 저장소에서 전달 됩니다.|

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여
Hello 솔루션 tooyour OMS 작업 영역에 추가 하면 hello **에이전트 상태** tooyour OMS 대시보드에 타일 추가 됩니다. 이 타일에서는 hello 에이전트의 총 수 및 응답 하지 않는 에이전트의 hello 수 hello 지난 24 시간 동안.<br><br> ![대시보드의 에이전트 상태 솔루션 타일](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Hello 클릭 **에이전트 상태** 타일 tooopen hello **에이전트 상태** 대시보드 합니다.  hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다. 각 열 hello에 대 한 열의 기준을 시간 범위를 지정 하는 일치 하는 수에 따라 hello 상위 10 개의 이벤트를 나열 합니다. 선택 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** 각 열의 또는 hello 열 머리글을 클릭 하 여 hello 오른쪽 아래에 있습니다.

| 열 | 설명 |
|--------|-------------|
| 시간에 따른 에이전트 수 | Linux 및 Windows 에이전트에 대해 7일 동안의 에이전트 수의 추세입니다.|
| 응답하지 않는 에이전트 개수 | 보내지 않은 하트 비트 hello에 지난 24 시간 동안은 에이전트의 목록입니다.|
| OS 형식별 배포 | 사용자 환경에 있는 Windows 및 Linux 에이전트 개수에 따른 분할입니다.|
| 에이전트 버전별 배포 | 사용자 환경 및 각각의 수에 설치 된 hello 다른 에이전트 버전의 파티션.|
| 에이전트 범주별 배포 | Hello 서로 다른 범주의 하트 비트 이벤트를 전송 하는 에이전트의 파티션을: 직접 에이전트, OpsMgr 에이전트 또는 hello OpsMgr 관리 서버입니다.|
| 관리 그룹별 배포 | Hello 사용자 환경에서 서로 다른 SCOM 관리 그룹의 파티션.|
| 에이전트의 지리적 위치 | 에이전트 및 각 국가에 설치 된 에이전트의 hello 수의 총 수가 있는 hello 다른 국가 파티션.|
| 설치된 게이트웨이 개수 | 설치 된 OMS 게이트웨이 hello와 이러한 서버 목록이 있는 서버의 hello 수입니다.|

![에이전트 상태 솔루션 대시보드 타일](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Log Analytics 레코드
hello 솔루션 hello OMS 리포지토리에 한 가지 유형의 레코드를 만듭니다.  

### <a name="heartbeat-records"></a>하트비트 레코드
**하트비트** 형식이 포함된 레코드가 만들어집니다.  이러한 레코드는 다음 표에 hello에 hello 속성이 있습니다.  

| 속성 | 설명 |
| --- | --- |
| 유형 | *하트비트*|
| Category | 값은 *직접 에이전트*, *SCOM 에이전트* 또는 *SCOM 관리 서버*합니다.|
| 컴퓨터 | 컴퓨터 이름입니다.|
| OSType | Windows 또는 Linux 운영 체제입니다.|
| OSMajorVersion | 운영 체제의 주 버전입니다.|
| OSMinorVersion | 운영 체제의 부 버전입니다.|
| 버전 | OMS 에이전트 또는 Operations Manager 에이전트 버전입니다.|
| SCAgentChannel | 값은 *직접* 및/또는 *SCManagementServer*합니다.|
| IsGatewayInstalled | OMS 게이트웨이가 설치된 경우 값은 *true*, 그렇지 않으면 *false*입니다.|
| ComputerIP | Hello 컴퓨터의 IP 주소입니다.|
| RemoteIPCountry | 컴퓨터가 배포된 지리적 위치입니다.|
| ManagementGroupName | Operations Manager 관리 그룹의 이름입니다.|
| SourceComputerId | 컴퓨터의 고유 ID입니다.|
| RemoteIPLongitude | 컴퓨터 지리적 위치의 경도입니다.|
| RemoteIPLatitude | 컴퓨터 지리적 위치의 위도입니다.|

보고 tooan Operations Manager 관리 서버는 두 개의 하트 비트를 보냅니다 및 SCAgentChannel 속성의 값에 모두 포함 하는 각 에이전트 **직접** 및 **SCManagementServer** 물품에 따라 로그 분석 데이터 원본 및 OMS 구독에서 설정한 솔루션입니다. 를 기억 하는 경우 솔루션의에서 데이터는 Operations Manager에서 직접 전송 관리 서버 toohello OMS 웹 서비스 또는 hello 인해 hello 에이전트에서 수집 된 데이터 볼륨 hello 에이전트 tooOMS 웹 서비스에서 직접 전송 됩니다. Hello 값을 포함 하는 하트 비트 이벤트에 대 한 **SCManagementServer**, hello ComputerIP 값 이므로 hello 관리 서버의 IP 주소 hello hello 데이터는 실제로에서 업로드 됩니다.  SCAgentChannel 너무 설정 되어 있는 하트 비트**직접**, hello hello 에이전트의 공용 IP 주소를 됩니다.  

## <a name="sample-log-searches"></a>샘플 로그 검색
hello 다음 표에서이 솔루션에 의해 수집 된 레코드에 대 한 예제 로그 검색.

| 쿼리 | 설명 |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |에이전트의 총수 |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |지난 24 시간 동안 hello에 응답 하지 않는 에이전트의 개수 |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |지난 15 분 동안 hello에 응답 하지 않는 에이전트의 개수 |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |컴퓨터 온라인 (지난 24 시간 동안 hello) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |총 에이전트 오프 라인에서 (지난 24 시간 동안 hello)에 대 한 지난 30 분 |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |시간에 따른 OSType별 에이전트 수의 추세 가져오기|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |OS 형식별 배포 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |에이전트 버전별 배포 |
| Type=Heartbeat&#124;measure count() by Category |에이전트 범주별 배포 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | 관리 그룹별 배포 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |에이전트의 지리적 위치 |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |설치된 OMS 게이트웨이 수 |


>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](../log-analytics/log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.
>
>| 쿼리 | 설명 |
|:---|:---|
| Heartbeat &#124; distinct Computer |에이전트의 총수 |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |지난 24 시간 동안 hello에 응답 하지 않는 에이전트의 개수 |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |지난 15 분 동안 hello에 응답 하지 않는 에이전트의 개수 |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |컴퓨터 온라인 (지난 24 시간 동안 hello) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |총 에이전트 오프 라인에서 (지난 24 시간 동안 hello)에 대 한 지난 30 분 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |시간에 따른 OSType별 에이전트 수의 추세 가져오기|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |OS 형식별 배포 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |에이전트 버전별 배포 |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |에이전트 범주별 배포 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | 관리 그룹별 배포 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |에이전트의 지리적 위치 |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |설치된 OMS 게이트웨이 수 |

## <a name="next-steps"></a>다음 단계

* Log Analytics에서 경고 생성에 대한 자세한 내용은 [Log Analytics의 경고](../log-analytics/log-analytics-alerts.md) 에 관하여 알아보세요.

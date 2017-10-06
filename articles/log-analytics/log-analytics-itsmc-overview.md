---
title: "OMS에서 서비스 관리 커넥터 aaaIT | Microsoft Docs"
description: "Hello IT 서비스 관리 커넥터 toocentrally 모니터를 사용 하 여 OMS에서는 hello ITSM 작업 항목을 관리 하며 모든 문제를 신속 하 게 해결 합니다."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>IT Service Management Connector(미리 보기)를 사용하여 ITSM 작업 항목을 중앙에서 관리

![IT Service Management Connector 기호](./media/log-analytics-itsmc/itsmc-symbol.png)

OMS 로그 분석 toocentrally 모니터에 hello IT 서비스 관리 (ITSMC) 커넥터를 사용 하 고 ITSM 제품/서비스 간에 작업 항목을 관리할 수 있습니다.

hello IT 서비스 관리 커넥터 OMS 로그 분석 기존 IT 서비스 관리 (ITSM) 제품 및 서비스를 통합합니다.  hello 솔루션 ITSM 제품/서비스와의 양방향 통합, OMS 사용자 옵션 toocreate 인시던트, 경고 또는 이벤트 ITSM 솔루션에서 제공 하는 경우 hello 지정 됩니다. 인시던트, 등의 데이터 가져오기도 수행 하는 hello 커넥터 및 OMS 로그 분석에 ITSM 솔루션에서 변경 요청 합니다.

IT Service Management Connector를 사용하여 다음을 수행할 수 있습니다.

  - 조직에서 사용되는 ITSM 제품/서비스에 대한 작업 항목을 중앙에서 모니터링 및 관리합니다.
  - OMS 경고 및 로그 검색을 통해 ITSM에서 ITSM 작업 항목(예: 경고, 이벤트, 인시던트)을 만듭니다.
  - ITSM 솔루션에서 인시던트 및 변경 요청을 읽고, Log Analytics 작업 영역에서 관련 로그 데이터와의 상관 관계를 파악합니다.
  - 예기치 않은 및 비정상적인 이벤트를 찾아 hello 최종 사용자가 호출 하 고 toohello 기술 지원팀 보고 하기 전에 해결 합니다.
  - 작업 항목 데이터를 Log Analytics로 가져오고 KPI(핵심 성과 지표) 보고서를 만듭니다.  이러한 보고서를 사용하여 중요한 일부 항목을 식별하고 평가한 후 맬웨어 평가와 같은 조치를 수행할 수 있습니다.
  - 엄선된 대시보드를 통해 인시던트, 변경 요청 및 영향 받은 시스템에 대한 심층 정보를 볼 수 있습니다.
  - Hello 로그 분석 작업 영역에서 다른 관리 솔루션으로 상호 연관 시켜 더 빠르게 문제를 해결 합니다.


## <a name="prerequisites"></a>필수 조건

tooimport hello ITSM 작업 항목 OMS 로그 분석에 hello 솔루션 hello 작업 항목을 가져올 있는 hello OMS의에서 IT 서비스 관리 커넥터 hello 및 hello IT SM 제품/서비스 간의 연결이 필요 합니다.


## <a name="configuration"></a>구성

에 설명 된 hello 프로세스를 사용 하 여 IT 서비스 관리 커넥터 솔루션 tooyour OMS 작업 공간에 추가 hello [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

IT 서비스 관리 커넥터 hello 솔루션 갤러리에 나와 있는 것 처럼 타일:

![커넥터 타일](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

성공적으로 추가 후 나타납니다에서 IT 서비스 관리 커넥터 hello **OMS** > **설정** > **연결 된 원본입니다.**

![ITSMC가 연결되어 있습니다.](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Hello IT 서비스 관리 커넥터 기본적으로 24 시간 마다 한 번에 hello 연결의 데이터를 새로 고칩니다. toorefresh 편집 또는 템플릿에 대 한 즉시 연결의 데이터 업데이트, 변경한 hello 새로 고침 단추 표시 다음 tooyour 연결을 클릭 합니다.

 ![ITSMC 새로 고침](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>관리 팩
이 솔루션에는 관리 팩이 필요하지 않습니다.

## <a name="connected-sources"></a>연결된 소스

hello 다음 ITSM 제품/서비스에서 지 원하는 IT 서비스 관리 커넥터 hello:

- [SCSM(System Center Service Manager)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello OMS IT 서비스 관리 커넥터를 ITSM 서비스에 연결 하면 hello 로그 분석 서비스에서 연결 하는 hello ITSM 제품/서비스 hello 데이터 수집을 시작 합니다.

> [!NOTE]
> - IT Service Management Connector 솔루션에서 가져온 데이터는 **ServiceDesk_CL**이라는 이벤트로 Log Analytics에 표시됩니다.
- 이벤트에는 **ServiceDeskWorkItemType_s**라는 필드가 포함됩니다. 으로 인시던트를 해당 값을 사용할 수 있습니다 또는 변경 요청, hello에 따라 작업 항목 hello에 포함 된 데이터는 **ServiceDesk_CL** 이벤트입니다.

## <a name="input-data"></a>데이터 입력
작업 hello ITSM 제품/서비스에서 가져온 항목입니다.

hello 다음 정보를 보여 줍니다 hello IT 서비스 관리 커넥터에 의해 수집 된 데이터의 예입니다.

> [!NOTE]
> Hello에 따라 작업 항목 형식으로 로그 분석 가져올 **ServiceDesk_CL** hello 다음 필드가 포함 되어 있습니다.

**작업 항목:** **인시던트**  
ServiceDeskWorkItemType_s="Incident"

**필드**

- ServiceDeskConnectionName
- 서비스 데스크 ID
- 시스템 상태
- 긴급도
- 영향
- 우선 순위
- 에스컬레이션
- 만든 사람
- 해결한 사람
- 종결한 사람
- 원본
- 할당 대상
- Category
- 제목
- 설명
- 만든 날짜
- 종결한 날짜
- 해결한 날짜
- 마지막으로 수정한 날짜
- 컴퓨터


**작업 항목:** **변경 요청**

ServiceDeskWorkItemType_s="ChangeRequest"

**필드**
- ServiceDeskConnectionName
- 서비스 데스크 ID
- 만든 사람
- 종결한 사람
- 원본
- 할당 대상
- 제목
- 형식
- Category
- 시스템 상태
- 에스컬레이션
- 충돌 상태
- 긴급도
- 우선 순위
- 위험
- 영향
- 할당 대상
- 만든 날짜
- 종결한 날짜
- 마지막으로 수정한 날짜
- 요청한 날짜
- 예상된 시작 날짜
- 예상된 종료 날짜
- 작업 시작 날짜
- 작업 종료 날짜
- 설명
- 컴퓨터

## <a name="output-data-for-a-servicenow-incident"></a>ServiceNow 인시던트에 대한 출력 데이터

| OMS 필드 | ITSM 필드 |
|:--- |:--- |
| ServiceDeskId_s| Number |
| IncidentState_s | 시스템 상태 |
| Urgency_s |긴급도 |
| Impact_s |영향|
| Priority_s | 우선 순위 |
| CreatedBy_s | 보고자 |
| ResolvedBy_s | 해결한 사람|
| ClosedBy_s  | 종결한 사람 |
| Source_s| 연락처 유형 |
| AssignedTo_s | 너무 할당 |
| Category_s | Category |
| Title_s|  간단한 설명 |
| Description_s|  참고 사항 |
| CreatedDate_t|  열림 |
| ClosedDate_t| closed|
| ResolvedDate_t|해결됨|
| 컴퓨터  | 구성 항목 |

## <a name="output-data-for-a-servicenow-change-request"></a>ServiceNow 변경 요청에 대한 출력 데이터

| OMS 필드 | ITSM 필드 |
|:--- |:--- |
| ServiceDeskId_s| Number |
| CreatedBy_s | 요청자 |
| ClosedBy_s | 종결한 사람 |
| AssignedTo_s | 너무 할당 |
| Title_s|  간단한 설명 |
| Type_s|  형식 |
| Category_s|  범주 |
| CRState_s|  시스템 상태|
| Urgency_s|  긴급도 |
| Priority_s| 우선 순위|
| Risk_s| 위험|
| Impact_s| 영향|
| RequestedDate_t  | 요청한 날짜 |
| ClosedDate_t | 종결한 날짜 |
| PlannedStartDate_t  |     예상된 시작 날짜 |
| PlannedEndDate_t  |   예상된 종료 날짜 |
| WorkStartDate_t  | 실제 시작 날짜 |
| WorkEndDate_t | 실제 종료 날짜|
| Description_s | 설명 |
| 컴퓨터  | 구성 항목 |

**ITSM 데이터에 대한 샘플 Log Analytics 화면:**

![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT Service Management Connector - 다른 OMS 솔루션과의 통합

현재 IT 서비스를 관리 하는 커넥터 서비스 맵 솔루션 hello와의 통합을 지원 합니다.

서비스 맵 Windows에서 응용 프로그램 구성 요소를 hello 및 Linux 시스템 및 지도 hello 서비스 간의 통신에 자동으로 검색 합니다. Tooview를 때 서버 –으로 볼 중요 한 서비스를 제공 하는 상호 연결 된 시스템 있습니다. 서비스 맵은 서버, 프로세스 및 에이전트 설치 이외에 구성이 필요 없는 TCP 연결 아키텍처의 포트 간 연결을 보여 줍니다. 추가 정보: [서비스 맵](../operations-management-suite/operations-management-suite-service-map.md)

이 통합을 hello 다음 예제와 같이 hello ITSM 솔루션에서 만든 hello 서비스 지원 센터 항목을 볼 수 있습니다.

![통합된 솔루션 ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>OMS 경고에 대한 ITSM 작업 항목 만들기

Hello OMS 경고에 대 한 연결 hello ITSM 소스에 연결 된 작업 항목을 만들 수 있습니다.  toodo 절차를 수행 하는이 사용 하 여 hello:

1. **로그 검색** 창 tooview 데이터를 로그 검색 쿼리를 실행 합니다. 쿼리 결과 작업 항목에 대 한 hello 소스입니다.
2. **로그 검색**, 클릭 **경고** tooopen hello **경고 규칙 추가** 페이지.

    ![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Hello에 **경고 규칙 추가** 창의 hello 필요한 세부 정보를 제공할 **이름**, **심각도**, **검색 쿼리**, 및  **경고 조건** (시간 창/메트릭 측정).
4. **ITSM 작업**에 대해 **예**를 선택합니다.
5. Hello에서 ITSM 연결을 선택 **연결 선택** 목록입니다.
6. 필요에 따라 hello 세부 정보를 제공 합니다.
7. 이 경고를 선택 하는 hello의 각 로그 항목에 대 한 별도 작업 항목 toocreate **각 로그 항목에 대 한 개별 작업 항목을 만들** 확인란을 선택 합니다.

    또는

    이 확인란을 선택 하지 않은 toocreate 하나의 작업 항목을 개수에 관계 없이 로그 항목에서이 경고에 대 한 상태로 둡니다.

7. **Save**를 클릭합니다.

hello OMS 경고는 만들어집니다 **경고**합니다. 안녕 해당 ITSM 연결의 작업 항목이 hello 지정한 경고 조건이 충족 되 면 생성 됩니다.

## <a name="create-itsm-work-items-from-oms-logs"></a>OMS 로그에서 ITSM 작업 항목 만들기

OMS 로그 검색을 사용 하 여 연결 하는 hello ITSM 소스에서 작업 항목을 만들 수 있습니다. toodo 절차를 수행 하는이 사용 하 여 hello:

1. **로그 검색**, hello 필요한 데이터를 검색, hello 세부 정보를 선택 하 고 클릭 **작업 항목 만들기**합니다.

    hello **ITSM 작업 만들기 항목** 창이 나타납니다.

    ![Log Analytics 화면](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Hello 다음 세부 정보를 추가 합니다.

  - **작업 항목 제목**: hello 작업 항목에 대 한 Title 합니다.
  - **작업 항목 설명**: hello 새 작업 항목에 대 한 설명입니다.
  - **컴퓨터에 영향을 받는**:이 로그 데이터를 찾을 수 hello 컴퓨터의 이름입니다.
  - **연결을 선택**: ITSM 연결 하려는 toocreate이 작업 항목.
  - **작업 항목**: 작업 항목의 유형입니다.

3. toouse 인시던트의 기존 작업 항목 템플릿을 클릭 **예** 아래 **생성 작업 항목 템플릿을 기반으로 hello** 옵션 선택한 다음 클릭 **만들기**합니다.

    또는

    클릭 **아니요** tooprovide 사용자 사용자 지정 된 값을 선택 합니다.

4. Hello hello에 적절 한 값을 제공 **연락처 유형**, **영향**, **긴급도**, **범주**, 및 **하위 범주**  텍스트 상자 및 클릭 **만들기**합니다.

OMS에서 볼 수 있습니다 ITSM hello에 hello 작업 항목이 생성 됩니다.

## <a name="troubleshoot-itsm-connections-in-oms"></a>OMS에서 ITSM 연결 문제 해결
1.  연결 된 소스 UI에서 연결이 실패 하 고 hello 얻게 **연결을 저장 하는 동안 오류가 발생 했습니다.** 메시지에서 다음 hello지 않습니다:
 - ServiceNow, Cherwell 및 Provance 연결의 경우 확인 하면 hello를 올바르게 입력 한 사용자 이름/암호 및 클라이언트 ID/클라이언트 암호 각 hello 연결에 대 한 합니다. Hello 오류가 계속 되 면 hello 해당 ITSM 제품 toomake hello 연결에서 충분 한 권한이 있는지 확인 합니다.
 - 서비스 관리자의 경우 확인 hello 웹 앱을 배포 했습니다. 하이브리드 연결을 만듭니다. tooverify hello 성공적으로 연결 hello 온-프레미스 서비스 관리자 컴퓨터와, hello를 만들기 위한 hello 설명서에 설명 된 대로 hello 웹 앱 URL을 방문 [하이브리드 연결](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)합니다.

2.  OMS에서 ServiceNow에서 데이터 동기화 시작 되지 않은, 해당 hello ServiceNow 인스턴스 중지 중이 아님를 확인 합니다. 이 발생할 수 있습니다 잠시 hello에 유휴 상태일 때 ServiceNow Dev 인스턴스. 다른 보고서 hello 문제가 발생 했습니다.
3.  OMS에서 경고를 가져오는 발생 하지만 작업 항목을 가져오는에서 ITSM 제품 또는 구성 항목 toowork 만든/연결 된 항목을 가져오지 않습니다. 만들거나 다음 hello 않는 일반 정보를:
 -  OMS 포털의 IT 서비스 관리 커넥터 솔루션에 사용 되는 tooget 연결/작업 항목/컴퓨터 등의 요약 될 수 있습니다. Hello 상태 블레이드에서 hello 오류 메시지, 너무 탐색**로그 검색** hello 오류 메시지에 hello 세부 정보를 사용 하 여 hello 오류가 있는 hello 연결을 확인 합니다.
 - hello에 hello 오류/관련 정보를 직접 볼 수 **로그 검색** 페이지를 사용 하 여 *유형 = ServiceDeskLog_CL*합니다.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Service Manager 웹앱 배포 문제 해결
1.  웹 앱 배포 문제를 발생 시 hello 구독에 대 한 충분 한 권한이 있는지 확인 toocreate/배포 하는 리소스를 설명 합니다.
2.  경우 **개체 참조가 개체의 tooinstance 설정 되지** hello를 실행 하는 동안 오류 메시지가 표시 됩니다. [스크립트](log-analytics-itsmc-service-manager-script.md) 에서 유효한 값을 입력 했는지 확인 **사용자 구성**섹션.
3.  Toocreate 서비스 버스 릴레이 네임 스페이스를 실패 한 경우 해당 hello 필요한 hello 구독에 리소스 공급자가 등록을 확인 합니다. 등록 되지 않은 경우 hello Azure 포털에서에서 만들 수동으로 합니다. 하지만 만들 수도 있습니다 [hello 하이브리드 연결을 만드는](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) hello Azure 포털에서에서 합니다.


## <a name="contact-us"></a>문의처

모든 쿼리 또는 hello IT 서비스 관리 커넥터에 대 한 피드백에 게 문의 하세요. [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com)합니다.

## <a name="next-steps"></a>다음 단계
[서비스 관리 커넥터 ITSM 제품/서비스 tooIT 추가](log-analytics-itsmc-connections.md)합니다.

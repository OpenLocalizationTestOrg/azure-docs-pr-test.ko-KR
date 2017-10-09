---
title: "aaaAdd Azure 로그 분석 관리 솔루션 | Microsoft Docs"
description: "OMS(Operations Management Suite)/Log Analytics 관리 솔루션은 특정 문제 영역을 중심으로 피벗된 메트릭을 제공하는 논리, 시각화 및 데이터 취득 규칙 컬렉션입니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Azure 로그 분석 관리 솔루션 tooyour 작업 영역 추가

Log Analytics 관리 솔루션은 특정 문제 영역을 중심으로 피벗된 메트릭을 제공하는 **논리**, **시각화** 및 **데이터 취득 규칙** 컬렉션입니다. 이 문서는 로그 분석에서 지 원하는 관리 솔루션을 나열 하 고 tooadd 및 제거를 사용 하 여 작업 영역에 대 한 Azure 포털을 hello 방법을 보여 줍니다. Hello 솔루션 갤러리를 사용 하 여 hello OMS 포털에서 솔루션을 추가할 수도 있습니다.

관리 솔루션을 사용하면:

* 운영 문제를 보다 빠르게 조사 및 해결하고,
* 다양한 유형의 컴퓨터 데이터를 수집 및 상호 연결하며,
* 도움말 hello 솔루션에 노출 하는 동작으로 예방할 수 있습니다.

> [!NOTE]
> 로그 분석 로그 검색 기능에 포함 되어 있으므로 관리 솔루션 tooenable tooinstall 필요가 없는 것입니다. 그러나 데이터 시각화, 추천된 검색어 및 얻게 insights 관리 솔루션 tooyour 작업 영역을 추가 하 여 합니다.

이 문서를 사용 하면 추가 hello Azure 포털 Marketplace 사용 하 여 관리 솔루션 tooa 작업 합니다. 솔루션을 추가한 후 데이터 hello 인프라의에서 서버에서 수집 되 고 toohello OMS 서비스로 전송 합니다. OMS 서비스는 일반적으로 몇 분 tooan 시간이 걸립니다 hello 하 여 처리 합니다. Hello 서비스가 hello 데이터를 처리 한 후에 OMS에서 볼 수 있습니다.

관리 솔루션이 더 이상 필요 없으면 손쉽게 제거할 수 있습니다. 관리 솔루션을 제거 하면 해당 데이터는 tooOMS 보내지 않습니다. Hello 무료 가격 책정 계층에 있는 경우는 솔루션을 제거 hello 데이터의 일일 할당량에서 유지 하는 데 사용 되는, 데이터 양을 줄일 수 있습니다.

## <a name="view-available-management-solutions"></a>사용할 수 있는 관리 솔루션 보기

hello Azure 마켓플레이스 목록이 포함 되어 hello [로그 분석에 대 한 관리 솔루션](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)합니다.

Hello를 클릭 하 여 Azure marketplace의 관리 솔루션을 설치할 수 있습니다 **지금 사용해 보세요** 각 솔루션의 hello 맨 아래에 링크 합니다.

## <a name="add-a-management-solution"></a>관리 솔루션 추가
1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com) Azure 구독을 사용 하 여 합니다.
2. Hello에 **새로** 아래 블레이드 **마켓플레이스**선택, **모니터링 + 관리**합니다.
3. Hello에 **모니터링 + 관리** 블레이드에서 클릭 **스크롤하게**합니다.  
    ![모니터링 + 관리 블레이드](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. 오른쪽 toohello **관리 솔루션**, 클릭 **자세한**합니다.
5. Hello에 **관리 솔루션** 블레이드에서 tooadd tooa 작업 영역을 지정 하는 관리 솔루션을 선택 합니다.  
    ![모니터링 + 관리 블레이드](./media/log-analytics-add-solutions/management-solutions.png)  
6. Hello 관리 솔루션 블레이드에서 hello 관리 솔루션에 대 한 정보를 검토 하 고 클릭 **만들기**합니다.
7. Hello에 *관리 솔루션 이름* 블레이드에서 원하는 tooassociate hello 관리 솔루션으로 작업 영역을 선택 합니다.
8. 필요에 따라 작업 영역 설정을 hello Azure 구독, 리소스 그룹 및 위치를 변경 합니다. **자동화 옵션**을 선택할 수도 있습니다. **만들기**를 클릭합니다.  
    ![솔루션 작업 영역](./media/log-analytics-add-solutions/solution-workspace.png)  
9. 사용자가 추가한 tooyour 작업 영역에서 hello 관리 솔루션을 사용 하 여 toostart 너무 이동**로그 분석** > **구독** > ***작업 영역 이름 ***  >  **개요**합니다. 관리 솔루션에 대한 새 타일이 표시됩니다. 고 hello 솔루션에 대 한 데이터가 수집 되 면 hello 솔루션을 사용 하 여 시작 hello 타일 tooopen를 클릭 합니다.

## <a name="remove-a-management-solution"></a>관리 솔루션 제거

1. Hello에 [Azure 포털](https://portal.azure.com), 너무 이동**로그 분석** > **구독** > ***작업 영역 이름을*** 한 다음 hello ***작업 영역 이름을*** 블레이드에서 클릭 **솔루션**합니다.
2. 관리 솔루션의 hello 목록의 tooremove hello 솔루션을 선택 합니다.
3. 작업 영역에 대 한 hello 솔루션 블레이드에서 클릭 **삭제**합니다.  
    ![솔루션 삭제](./media/log-analytics-add-solutions/solution-delete.png)  
4. Hello 확인 대화 상자에서 클릭 **예**합니다.

## <a name="offers-and-pricing-tiers"></a>제품 및 가격 책정 계층

다음 표에서 hello 관리 솔루션 속한 tooeach Operations Management Suite 제품을 식별 합니다.
hello 테이블에는 각 관리 솔루션에 사용할 수 있는 가격대 hello를 식별 합니다.
다음 표에 hello에서 모든 솔루션은 hello hello 로그 분석 포털에서 Azure 포털 및 hello 솔루션 갤러리 내에서 사용할 수 있습니다.

| 관리 솔루션                                                                       | 제안                                                                     | 가격 책정 계층<sup>1</sup>                                                 | 참고 사항 |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)(활동 로그 분석)                                                                   | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | 90일간 데이터 무료 제공<br>데이터 대상이 아닙니다. 무료 계층 캡 toohello |
| [AD 평가](log-analytics-ad-assessment.md)                                           | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [AD 복제 상태](log-analytics-ad-replication-status.md)                           | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [에이전트 상태](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | 데이터 대상이 아닙니다. 무료 계층 캡 toohello<br> Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [경고 관리](log-analytics-solution-alert-management.md)                            | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [Application Insights 커넥터(미리 보기)](log-analytics-app-insights-connector.md)                                               | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Automation Hybrid Worker](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>자동화 및 제어</li></ul>                                  | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다. |
| [Azure Application Gateway 분석](log-analytics-azure-networking-analytics.md)    | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Azure 네트워크 보안 그룹 분석](log-analytics-azure-networking-analytics.md)     | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Azure SQL Analytics(미리 보기)](log-analytics-azure-sql.md)                                                       | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br>&nbsp;노드당&nbsp;(OMS)                                                                          | 로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다.|
| [Azure Web Apps 분석](log-analytics-azure-web-apps-analytics.md)     | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
|[백업](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)                                                                       | 기존 백업 자격 증명 모음이 필요합니다.<br> Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [용량 및 성능(미리 보기)](log-analytics-capacity.md)                                                   | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [변경 내용 추적](log-analytics-change-tracking.md)                                       | <ul><li>자동화 및 제어</li></ul>                                  | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다. |
| [컨테이너](log-analytics-containers.md)                                                 | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [IT Service Management Connector(미리 보기)](log-analytics-itsmc-overview.md)                                              | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> &nbsp;노드당&nbsp;(OMS)     | |
| HDInsight HBase 모니터링 <br>(미리 보기)                                                  | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Key Vault 분석](log-analytics-azure-key-vault.md)                   | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [맬웨어 평가](log-analytics-malware.md)                                            | <ul><li>보안 및 규정 준수</li></ul>                                 | 무료<br> 독립 실행형<br>&nbsp;노드당&nbsp;(OMS)                                                                           | 2017 년 6 월 19 후 hello 보안 및 규정 준수 솔루션에 추가할 경우 [노드당 청구는](https://azure.microsoft.com/pricing/details/security-compliance/)hello 작업 영역 가격 책정 계층에 관계 없이 합니다. hello 처음 60 일 동안 사용할 수 있는 합니다.  |
| [네트워크 성능 모니터](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight and Analytics</li></ul>                                   | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | |
| [Office 365 분석(미리 보기)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [보안 및 감사](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>보안&nbsp;및&nbsp;규정 준수</li></ul>                       | 무료<br> 독립 실행형<br>&nbsp;노드당&nbsp;(OMS)                                                                           | 보안 이벤트 로그를 수집하려면 이 솔루션이 필요<br>2017 년 6 월 19 후 hello 보안 및 규정 준수 솔루션에 추가할 경우 [노드당 청구는](https://azure.microsoft.com/pricing/details/security-compliance/)hello 작업 영역 가격 책정 계층에 관계 없이 합니다. hello 처음 60 일 동안 사용할 수 있는 합니다. |
| [Service Fabric 분석(미리 보기)](log-analytics-service-fabric.md)                     | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [서비스 맵(미리 보기)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight and Analytics</li></ul>                      | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 미국 동부, 유럽 서부 및 미국 중서부에서 사용 가능    |
| [사이트 복구](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight and Analytics</li></ul>                                   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)                                                                       | 기존 Site Recovery 자격 증명 모음이 필요합니다.<br> Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [SQL 평가](log-analytics-sql-assessment.md)                                         | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| 작업이 없는 동안 VM 시작/중지<br>(미리 보기)                                              | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다. |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [System Center Operations Manager 평가(미리 보기)](log-analytics-scom-assessment.md)  | <ul><li>Insight and Analytics</li><li>Log Analytics</li></ul>        | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [업데이트 관리](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>자동화 및 제어</li></ul>                                  | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다. |
| [업데이트 준수(미리 보기)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | 데이터 또는 노드 무료 사용<br>데이터는 toohello 무료 계층 캡을 대상이 아닙니다.<br> Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [업그레이드 준비](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | 데이터 또는 노드 무료 사용<br>데이터는 toohello 무료 계층 캡을 대상이 아닙니다.<br> Azure 포털/마켓플레이스에서 tooadd 사용할 수 없습니다. |
| [VMware 모니터링(미리 보기)](log-analytics-vmware.md)                                | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> Standard<br> Premium&nbsp;(OMS)<br> &nbsp;GB당&nbsp;(독립 실행형)<br> &nbsp;노드당&nbsp;(OMS)   | |
| [Wire Data 2.0(미리 보기)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | 무료<br> &nbsp;노드당&nbsp;(OMS)                                                                         | 미국 동부, 유럽 서부 및 미국 중서부에서 사용 가능 |

<sup>1</sup> hello *표준* 및 *Premium (OMS)* 가격 책정 계층은만 자신의 로그 분석 작업 영역 이전 tooSeptember 21, 2016 만든 고객을 위해 사용할 수 있습니다.

### <a name="community-provided-management-solutions"></a>커뮤니티 제공 관리 솔루션

Hello에서 사용할 수 있는 커뮤니티 제공 솔루션 [Azure 템플릿 갤러리](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) 및 hello 작성자가 직접 합니다.

| 관리 솔루션               | 제안                                                                     | 가격 책정 계층                         | 메모 |
| ---                               | ---                                                                       | ---                                   | ---   |
| 모든 커뮤니티 제공 솔루션  | <ul><li>정보&nbsp;및&nbsp;분석</li><li>Log Analytics</li></ul>   | 무료<br> &nbsp;노드당&nbsp;(OMS)     |   로그 분석 작업 영역 연결 toobe tooan 자동화 계정이 필요합니다. |




## <a name="data-collection-details"></a>데이터 수집 세부 정보
hello 다음 표에서 보여 데이터 수집 방법과 및 로그 분석 관리 솔루션 및 데이터 원본에 대 한 데이터 수집 방법에 대 한 기타 세부 정보입니다. hello 테이블은에 의해 분류 결과가 너무 솔루션 제안,[구독 가격 책정 계층이](https://go.microsoft.com/fwlink/?linkid=827926)합니다. 활동 로그 분석 솔루션 hello 가격 책정 계층을 무료로 사용할 수 있는 tooall입니다.

로그 분석 Windows 에이전트 hello 및 System Center Operations Manager 에이전트는 기본적으로 hello 동일 합니다. 추가 기능 tooallow를 포함 하는 hello Windows 에이전트 것 tooconnect toohello OMS 작업 영역 및 프록시를 통해 경로입니다. Operations Manager 에이전트를 사용 하는 경우 oms는 OMS 에이전트 toocommunicate로 대상 해야 합니다. 이 테이블의 operations Manager 에이전트는 OMS 에이전트는 연결 된 tooOperations 관리자입니다. 참조 [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md) 에 기존 Operations Manager 환경 tooOMS 연결에 대 한 정보에 대 한 합니다.

> [!NOTE]
> 사용 하는 에이전트 hello 유형에 따라 데이터 전송 방법을 tooOMS, 조건에 따라 hello로 결정 됩니다.
> - Hello Windows 에이전트 또는 Operations Manager 연결 된 OMS 에이전트 사용 하거나 있습니다.
> - Operations Manager 요구 되는 경우 hello 솔루션에 대 한 Operations Manager 에이전트 데이터는 항상 tooOMS hello Operations Manager 관리 그룹을 사용 하 여 전송 합니다. 또한 Operations Manager 필요할 때만 hello Operations Manager 에이전트는 hello 솔루션에서 사용 됩니다.
> - TooOMS 관리 그룹을 사용 하는 경우 Operations Manager 필요 하지 않으며 hello 표에서 Operations Manager 에이전트 데이터가 tooOMS hello 관리 그룹을 Operations Manager 에이전트 데이터 전송 된다는 항상 전송 됩니다. Windows 에이전트 hello 관리 그룹을 무시 하 고 해당 데이터 보내기 직접 tooOMS 합니다.
> - Operations Manager 에이전트 데이터는 관리 그룹을 사용 하 여 전송 되지 다음 hello 데이터가 전송 않으므로 직접 tooOMS-hello 관리 그룹을 무시 합니다.

### <a name="insight--analytics--log-analytics"></a>정보 및 분석/Log Analytics

| 관리 솔루션 | 플랫폼 | Microsoft Monitoring Agent | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Activity Log Analytics | Azure |   |   |   |   |   | 알림 시 |
| AD 평가 |Windows |&#8226; |&#8226; |  |  |&#8226; |7 일 |
| AD 복제 상태 |Windows |&#8226; |&#8226; |  |  |&#8226; |5일 |
| 에이전트 상태 | Windows 및 Linux | &#8226; | &#8226; |   |   | &#8226; | 1분 |
| 경고 관리(Nagios) |Linux |&#8226; |  |  |  |  |도착 시 |
| 경고 관리(Zabbix) |Linux |&#8226; |  |  |  |  |1분 |
| 경고 관리(Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3분 |
| Application Insights 커넥터(미리 보기) | Azure |   |   |   |   |   | 알림 시 |
| Azure Application Gateway 분석 | Azure |   |   |   |   |   | 알림 시 |
| Azure 네트워크 보안 그룹 분석 | Azure |   |   |   |   |   | 알림 시 |
| Azure SQL Analytics(미리 보기) |Windows |  |  |  |  |  | 10분 |
| 용량 관리 |Windows |&#8226; |&#8226; |  |  |&#8226; |도착 시 |
| 컨테이너 | Windows 및 Linux | &#8226; | &#8226; |   |   |   | 3분 |
| Key Vault 분석 |Windows |  |  |  |  |  |알림 시 |
| 네트워크 성능 모니터 | Windows | &#8226; | &#8226; |   |   |   | TCP는 5초마다 핸드셰이크를 수행하며 3분마다 데이터가 전송됩니다. |
| Office 365 분석(미리 보기) |Windows |  |  |  |  |  |알림 시 |
| Service Fabric 분석 |Windows |  |  |&#8226; |  |  |5분 |
| 서비스 맵 | Windows 및 Linux | &#8226; | &#8226; |   |   |   | 15초 |
| SQL 평가 |Windows |&#8226; |&#8226; |  |  |&#8226; |7 일 |
| SurfaceHub |Windows |&#8226; |  |  |  |  |도착 시 |
| System Center Operations Manager 평가(미리 보기) | Windows | &#8226; | &#8226; |   |   | &#8226; | 7일 |
| Analytics 업그레이드(미리 보기) | Windows | &#8226; |   |   |   |   | 2일 |
| VMware 모니터링(미리 보기) | Linux | &#8226; |   |   |   |   | 3분 |
| 실시간 데이터 |Windows(2012 R2/8.1 이상) |&#8226; |&#8226; |  |  |  | 1분 |


### <a name="automation--control"></a>Automation and Control

| 관리 솔루션 | 플랫폼 | Microsoft Monitoring Agent | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automation Hybrid Worker | Windows | &#8226; | &#8226; |   |   |   | 해당 없음 |
| 변경 내용 추적 |Windows |&#8226; |&#8226; |  |  |&#8226; |매시간 |
| 변경 내용 추적 |Linux |&#8226; |  |  |  |  |매시간 |
| 업데이트 관리 | Windows |&#8226; |&#8226; |  |  |&#8226; |하루에 최소 2회 및 업데이트를 설치하고 15분 후 |

### <a name="security--compliance"></a>보안 및 규정 준수

| 관리 솔루션 | 플랫폼 | Microsoft Monitoring Agent | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 맬웨어 방지 평가 |Windows |&#8226; |&#8226; |  |  |&#8226; |매시간 |
| 보안 및 감사<sup>1</sup> | Windows 및 Linux | 부분 | 부분 | 부분 |   | 부분 | 다양 |

<sup>1</sup> hello 보안 및 감사 솔루션 창, Operations Manager 및 Linux 에이전트에서 로그를 수집할 수 있습니다. 다음 항목에 대한 데이터 수집 정보는 [데이터 원본](#data-sources)을 참조하세요.

- syslog
- Windows 보안 이벤트 로그
- Windows 방화벽 로그
- Windows 이벤트 로그



### <a name="protection--recovery"></a>보호 및 복구

| 관리 솔루션 | 플랫폼 | Microsoft Monitoring Agent | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 백업 | Azure |   |   |   |   |   | 해당 없음 |
| Azure Site Recovery | Azure |   |   |   |   |   | 해당 없음 |


### <a name="data-sources"></a>데이터 원본


| 데이터 원본 | 플랫폼 | Microsoft Monitoring Agent | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Azure 활동 로그 |Windows |  |  |  |  |  |알림 시 |
| Azure 진단 로그 |Windows |  |  |  |  |  |알림 시 |
| Azure 진단 메트릭 |Windows |  |  |  |  |  |알림 시 |
| ETW |Windows |  |  |&#8226; |  |  |5분 |
| IIS 로그 |Windows |&#8226; |&#8226; |&#8226; |  |  |5분 |
| 성능 카운터 |Windows |&#8226; |&#8226; |  |  |  |예약된 대로, 최소 10초 |
| 성능 카운터 |Linux |&#8226; |  |  |  |  |예약된 대로, 최소 10초 |
| syslog |Linux |&#8226; |  |  |  |  |Azure 저장소: 10분, 에이전트: 도착 시 |
| Windows 보안 이벤트 로그 |Windows |&#8226; |&#8226; |&#8226; |  |  |Azure 저장소: 10 분입니다. hello 에이전트: 도착 시 |
| Windows 방화벽 로그 |Windows |&#8226; |&#8226; |  |  |  |도착 시 |
| Windows 이벤트 로그 |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |Azure 저장소: 10 분입니다. hello 에이전트: 도착 시 |



## <a name="preview-management-solutions-and-features"></a>미리 보기 관리 솔루션 및 기능
서비스를 실행 하 고 devops 사례를 고객 toodevelop 기능 및 솔루션 toopartner를 수 있습니다.

비공개 미리 보기 동안 म 지정 소규모 그룹의 고객 액세스 tooan hello 기능 또는 솔루션 toogain 피드백의 초기 구현 하 고 개선 합니다. 이 초기 구현에는 최소한의 기능 및 운영 기능이 있습니다.

이러한 목표 이므로 tootry 작업 신속 하 게 작동 기능 및 작동 하지 않는 항목을 찾을 수 있습니다. म hello 비공개 미리 보기 고객의 의견 hello 있다는 메시지가 저희가 공개 미리 보기에 대 한 준비 될 때까지이 프로세스가 반복 합니다.

Hello 공개 미리 보기 중 hello 기능 또는 솔루션에 사용할 수 있도록 모든 사용자가 tooget 자세한 피드백 것을 우리의 확장 및 효율성을 검사 합니다. 이 단계 동안:

* 미리 보기 기능 hello 설정 탭에 표시 되며 모든 사용자가 사용 하도록 설정할 수 있습니다.
* 미리 보기 솔루션은 추가 hello 갤러리 또는 스크립트를 사용 하 여 합니다.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>미리 보기 기능 및 솔루션에 대해 무엇을 알아야 하나요?
새로운 기능 및 관리 솔루션에 대 한 기능 및 toodevelop 하면 해당 작업를 포함 합니다.

미리 보기 기능 및 솔루션이 모든 사용자에 적합한 것은 아닙니다. 를 toojoin 비공개 미리 보기 버전을 요청 하거나 공개 미리 보기를 사용 하도록 설정 하기 전에 개발 중인 있는 항목으로 작업 하는 확인 해야 합니다.

Hello 포털을 통해 미리 보기 기능을 사용 하는 경우 미리 보기에는 hello 기능을 알리는 경고 볼 수 있습니다.

#### <a name="for-both-private-and-public-preview"></a>*비공개* 및 *공개* 미리 보기의 경우
hello 다음 정보가 적용 tooboth 공개 및 비공개 미리 보기:

* 항상 올바르게 작동하지 않을 수 있습니다.
  * 전혀 작동 하지 않는 toosomething 통해 부 사태 되는 범위를 발급 합니다.
* Hello 미리 보기 toohave 시스템에 부정적인 영향 발생할 / 환경입니다.
  * OMS 하지만 경우에 따라 예기치 않은 작업을 사용 하는 상황이 발생 toohello 시스템 발생 tooavoid 음수 작업 시도 합니다.
* 데이터 손실.손상이 발생할 수 있습니다.
* 에서는 문제를 해결 하면 toocollect 진단 로그 또는 기타 데이터 toohelp 요청할 수 있습니다.
* (일시적 또는 영구적으로) hello 기능 또는 솔루션을 제거할 수 있습니다.
  * Hello 미리 보기 동안 지식을에 따른 म toonot 릴리스 hello 기능 또는 솔루션을 결정할 수 있습니다.
* 미리 보기는 작동하지 않거나 모든 구성으로 테스트되지 않을 수 있으며 다음을 제한할 수도 있습니다.
  * hello 사용할 수 있는 운영 체제 (예를 들어 기능만 부과 가능 tooLinux 미리 보기에 있는 동안).
  * hello 사용할 수 있는 agent (MMA, Operations Manager)의 유형 (예를 들어 기능 하지 못할 미리 보기에서 작업 하는 동안 Operations Manager와 함께).  
* 미리 보기 솔루션 및 기능 hello 서비스 수준 계약 설명 하지 않습니다.
* 미리 보기 기능을 사용하면 사용 요금이 발생합니다.
* 기능 또는 기능 hello 기능에 필요한 / 누락 되었거나 불완전 한 솔루션 toobe 유용할 수 있습니다.
* 기능/솔루션은 모든 지역에서 사용하지 못할 수도 있습니다.
* 기능/솔루션을 지역화되지 않을 수 없습니다.
* 기능 / 솔루션 hello 고객이 나 사용할 수 있는 장치 수에 제한이 있습니다.
* Toouse 스크립트 tooperform 구성과 tooenable hello 솔루션/기능 할 수 있습니다.
* hello UI (사용자 인터페이스) 완전 하지 않으며 하루 tooday에서 변경 될 수 있습니다.
* 공개 미리 보기는 프로덕션/중요 시스템에 적합하지 않을 수 있습니다.

#### <a name="for-private-preview"></a>*비공개* 미리 보기의 경우
또한 toohello 위의 항목, 다음 정보는 hello 특정 tooprivate 미리 보기입니다.

* 경험에 대 한 의견을 주세요. म 내릴 수 있도록 hello 기능/솔루션 더 잘 tooprovide를 생각 됩니다.
* 설문 조사, 전화 또는 전자 메일을 사용하여 피드백에 관해 연락을 드릴 수 있습니다.
* 기능이 항상 올바르게 작동하지는 않습니다.
* 참여에 대한 비밀 유지 계약(NDA)을 요구하거나 기밀 콘텐츠를 포함할 수 있습니다.
  * 블로깅 tweeting, 또는 제 3 자와 그렇지 않은 경우 통신을 하기 전에 확인 하십시오 hello 미리 보기 toounderstand 담당 하는 프로그램 관리자 hello로 노출에 대 한 제한을.
* 프로덕션/중요 시스템에서 실행하지 마십시오.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>액세스 tooprivate 미리 보기 기능 및 솔루션 얻는 방법
Hello 미리 보기에 따라 여러 가지 방법으로 통해 고객 tooprivate 미리 보기 초대합니다.

* Hello 월별 고객 설문 조사 응답 하 고을 버리고 우리 권한 toofollow 있습니다 가능성을 초대 된 tooa 비공개 미리 보기 되 고 향상 됩니다.
* Microsoft 계정 팀은 사용자를 지정할 수 있습니다.
* Twitter [msopsmgmt](https://twitter.com/msopsmgmt)에 게시된 세부 정보에 따라 등록할 수 있습니다.
* 자세한 공유 커뮤니티 이벤트에 따라 등록할 수 있습니다. 밋업, 회의 및 온라인 커뮤니티에서 찾아보세요.

## <a name="next-steps"></a>다음 단계
* [로그 검색](log-analytics-log-searches.md) tooview 관리 솔루션에서 수집 된 정보를 자세히 설명 합니다.

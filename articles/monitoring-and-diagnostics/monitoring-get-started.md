---
title: "aaaGet Azure 모니터 시작 | Microsoft Docs"
description: "리소스의 hello 작업에 대 한 Azure 모니터 toogain 정보를 사용 하 여 시작 하 고 데이터 기반으로 하는 작업을 수행 합니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Azure Monitor 시작
Azure 모니터는 Azure 리소스를 모니터링 하기 위한 단일 소스를 제공 하는 hello 플랫폼 서비스입니다. Azure 모니터를 사용 시각화, 쿼리, 경로, 보관 하 고 수 hello 메트릭 및 Azure의에서 리소스에서 오는 로그 작업을 수행 합니다. Hello 모니터 포털 블레이드를 사용 하 여이 데이터를 사용 하 여 작업할 수 [모니터 PowerShell Cmdlet](insights-powershell-samples.md), [플랫폼 간 CLI](insights-cli-samples.md), 또는 [Azure 모니터 REST Api](https://msdn.microsoft.com/library/dn931943.aspx)합니다. 이 문서에서는 몇 가지 hello 데모 hello 포털을 사용 하 여 Azure 모니터의 주요 구성 요소를 통해 진행 합니다.

1. Hello 포털에서 이동 너무**더 많은 서비스** hello 및 **모니터** 옵션입니다. Hello 왼쪽의 탐색 모음에서 쉽게 액세스할 수는 항상 되도록 hello 별 모양 아이콘 tooadd 옵션 tooyour 즐겨찾기 목록에이 클릭 합니다.
   
    ![Hello 서비스 목록에서 모니터링](./media/monitoring-get-started/monitor-more-services.png)
2. Hello 클릭 **모니터** hello 옵션 tooopen **모니터** 블레이드입니다. 이 블레이드에서는 모든 모니터링 설정과 데이터를 하나의 통합 보기로 모읍니다. Toohello를 처음 열면 **활동 로그** 섹션.
   
    ![모니터 블레이드 탐색](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Azure 모니터에 모니터링 데이터의 세 가지 기본 범주가: hello **활동 로그**, **메트릭**, 및 **진단 로그**합니다.
3. 클릭 **활동 로그** 활동 로그 섹션 hello tooensure 표시 됩니다.
   
    ![활동 로그 블레이드](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    hello [ **활동 로그** ](monitoring-overview-activity-logs.md) 구독의 리소스에에서 대해 수행 된 모든 작업에 설명 합니다. Hello 활동 로그를 사용 하 여 hello 확인할 수 있습니다 ' 부분, who, 시기 및 ' 모든 만들기에 대 한 업데이트 또는 구독의 리소스에에서 대 한 작업을 삭제 합니다. 예를 들어 hello 활동 로그를 표시 하면 웹 앱이 중지 되었습니다 중지는 합니다. 활동 이벤트 로그는 90 일 동안 hello 플랫폼 및 사용 가능한 tooquery에 저장 됩니다.
   
    수 만들고 저장 pin hello 가장 중요 한 쿼리 tooa 포털 대시보드에서 한 공통 필터 다음에 대 한 쿼리 조건을 충족 하는 이벤트가 발생 한 경우 항상 변경할 수 있습니다.
4. 지난 주 hello를 통해 hello tooa 특정 리소스 그룹 보기를 필터링 한 다음 클릭 hello **저장** 단추입니다.
   
    ![활동 로그 쿼리 저장](./media/monitoring-get-started/monitor-act-log-save.png)
5. 이제 hello 클릭 **Pin** 단추입니다.
   
    ![활동 로그에 대한 고정 클릭](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    대부분의 hello 보기가이 연습에서 고정 된 tooa 대시보드 될 수 있습니다. 이렇게 하면 서비스에 대한 운영 데이터 정보를 제공하는 단일 출처를 만들 수 있습니다. 
6. Tooyour 대시보드를 반환 합니다. 이제 hello 쿼리 (및 결과의 수) 대시보드에서 표시 되는지 확인할 수 있습니다. Tooquickly 참조에서에서 발생 한 최근 구독, 예: 뚜렷한 행위를 원하는 경우에 유용 합니다. 새 역할 할당 또는 VM 삭제 되었습니다.
   
    ![활동 로그 고정 toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Toohello 반환 **모니터** 타일을 클릭 하는 hello **메트릭** 섹션. 먼저 필터링 하 고 hello hello 블레이드 위쪽에 hello 드롭다운 옵션을 사용 하 여 선택 하 여 리소스 tooselect을 해야 합니다.
   
    ![메트릭에 대한 리소스 필터링](./media/monitoring-get-started/monitor-met-filter.png)
   
    모든 Azure 리소스에서 [**메트릭**](monitoring-overview-metrics.md)을 내보냅니다. 이 보기는 리소스에서 수행하는 방식을 쉽게 이해할 수 있도록 모든 메트릭을 단일 창에 모아 놓습니다.
8. 리소스를 선택 하면 사용 가능한 모든 메트릭이 hello hello 블레이드의 왼쪽에 표시 됩니다. 메트릭 선택 하 여 한 번에 여러 가지 메트릭을 차트 고 hello 그래프 종류 및 시간 범위를 수정할 수 있습니다. 이 리소스에 대해 설정한 모든 메트릭 경로도 확인할 수 있습니다.
   
    ![메트릭 블레이드](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > 일부 메트릭은 리소스에 대해 [Application Insights](../application-insights/app-insights-overview.md) 및/또는 Windows/Linux Azure 진단을 사용하도록 설정한 경우에만 사용할 수 있습니다.
   > 
   > 
9. 만족할 경우 차트를 hello 사용할 수 있습니다 **Pin** 단추 toopin 것 tooyour 대시보드 합니다.
10. Toohello 반환 **모니터** 블레이드에 대 한 클릭 **진단 로그**합니다.
    
    ![진단 로그 블레이드](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**진단 로그** ](monitoring-overview-of-diagnostic-logs.md) 내보내집니다 로그는 *여* 해당 리소스의 hello 작업에 대 한 데이터를 제공 하는 리소스입니다. 예를 들어 네트워크 보안 그룹 규칙 카운터와 논리 앱 워크플로 로그는 모두 진단 로그의 형식입니다. 이러한 로그를 스트리밍된 tooan 이벤트 허브 저장소 계정에 저장 하거나 전송 수[로그 분석](../log-analytics/log-analytics-overview.md)합니다. Log Analytics는 고급 검색 및 경고를 위한 Microsoft의 운영 인텔리전스 제품입니다.
    
    Hello 포털에서 볼 수 있으며 진단 로그를 사용할 수 있는 경우 구독 tooidentify에서 모든 리소스의 목록을 필터링 키를 누릅니다.
11. Hello 진단 로그 블레이드에서 리소스를 클릭 합니다. 진단 로그가 저장소 계정에 저장된 경우 직접 다운로드할 수 있는 시간별 로그 목록이 표시됩니다.
    
    ![하나의 리소스에 대한 진단 로그](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    클릭할 수도 있습니다 **진단 설정을**를 tooset 사용 하면 있으며 tooEvent 허브 스트리밍 또는 tooa 로그 분석 작업 영역을 보내는 tooa 보관 저장소 계정에 대 한 설정을 수정 합니다.
    
    ![진단 로그 활성화](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    에 진단 로그 tooLog Analytics 설정 하는 경우 다음에서 검색할 수 있습니다 이러한 hello **로그 검색** hello 포털의 섹션입니다.
12. Toohello 이동 **경고** hello 모니터 블레이드의 섹션입니다.
    
    ![공용 경고 블레이드](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    여기서 Azure 리소스에 대한 모든 [**경고**](monitoring-overview-alerts.md)를 관리할 수 있습니다. 여기에는 메트릭, 활동 로그 이벤트, Application Insights 웹 테스트(위치) 및 Application Insights 사전 진단에 대한 경고가 포함됩니다. 경고는 전자 메일 toobe 전송 또는 HTTP POST tooa webhook URL을 트리거할 수 있습니다.
13. 클릭 **추가 메트릭 경고** toocreate 경고 합니다.
    
    ![메트릭 경고 추가](./media/monitoring-get-started/monitor-alerts-add.png)
    
    Pin 경고 tooyour 대시보드 tooeasily 언제 든 지 해당 상태를 볼 수 있습니다.
14. hello 모니터 섹션도 포함 되어 링크 너무[Application Insights](../application-insights/app-insights-overview.md) 응용 프로그램 및 [로그 분석](../log-analytics/log-analytics-overview.md) 관리 솔루션입니다. 이러한 다른 Microsoft 제품은 Azure Monitor와 자연스럽게 통합됩니다.
15. Application Insights나 Log Analytics를 사용하지 않을 경우 기존 모니터링, 로깅, 경고 제품과 Azure Monitor를 함께 사용할 수 있습니다. 참조 우리의 [파트너 페이지](monitoring-partners.md) 전체 목록 및 방법에 대 한 지침에 대 한 toointegrate 합니다.

다음 단계를 수행 하 고 모든 관련 타일 tooa 대시보드에 고정 하 여 이와 같은 인프라 및 응용 프로그램의 포괄적인 뷰를 만들 수 있습니다.

![Azure Monitor 대시보드](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>다음 단계
* 읽기 hello [Azure 모니터 개요](monitoring-overview.md)


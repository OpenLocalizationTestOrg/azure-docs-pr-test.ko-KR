---
title: "Log Analytics 새 로그 검색 질문과 대답 | Microsoft 문서"
description: "이 문서에서는 Log Analytics를 새 쿼리 언어로 업그레이드하는 과정과 관련된 질문과 대답을 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: d7bd0d780c265cc15ad09a73ede8c5a886005e37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Log Analytics 새 로그 검색 FAQ 및 알려진 문제

이 문서에는 [새 쿼리 언어로의 Log Analytics](log-analytics-log-search-upgrade.md) 업그레이드와 관련한 질문과 대답 및 알려진 문제가 포함되어 있습니다.  작업 영역을 업그레이드하도록 결정하기 전에 이 전체 문서를 읽어야 합니다.


## <a name="alerts"></a>경고

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-to-create-them-again-in-the-new-language-after-i-upgrade"></a>질문: 경고 규칙이 매우 많습니다. 업그레이드 후에 새 언어로 규칙을 다시 만들어야 하나요?  
아니요, 경고 규칙은 업그레이드 중에 새 검색 언어로 자동 변환됩니다.  


## <a name="computer-groups"></a>컴퓨터 그룹

### <a name="question-im-getting-errors-when-trying-to-use-computer-groups--has-their-syntax-changed"></a>질문: 컴퓨터 그룹을 사용하려고 할 때 오류가 발생합니다.  구문이 변경되었나요?
예, 작업 영역이 업그레이드될 때 컴퓨터 그룹을 사용하는 구문이 변경됩니다.  자세한 내용은 [Log Analytics 로그 검색의 컴퓨터 그룹](log-analytics-computer-groups.md)을 참조하세요.

### <a name="known-issue-groups-imported-from-active-directory"></a>알려진 문제: Active Directory에서 가져온 그룹
현재 Active Directory에서 가져온 컴퓨터 그룹을 사용하는 쿼리를 만들 수 없습니다.  해결 방법으로, 이 문제를 해결할 때까지 가져온 Active Directory 그룹을 사용하여 새 컴퓨터 그룹 만든 다음, 쿼리에 해당 새 그룹을 사용하는 것입니다.

가져온 Active Directory 그룹을 포함하는 새 컴퓨터 그룹을 만드는 쿼리의 예는 다음과 같습니다.

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>대시보드

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>질문: 대시보드를 업그레이드된 작업 영역에서 계속 사용할 수 있나요?
작업 영역을 업그레이드하기 전에 추가한 **내 대시보드**를 계속 사용할 수 있습니다. 하지만 해당 타일을 편집하거나 새로 만들 수는 없습니다.  [뷰 디자이너](log-analytics-view-designer.md)로 뷰를 계속 만들고 편집할 수 있으며, Azure Portal에서 대시보드를 만들 수도 있습니다.


## <a name="log-searches"></a>로그 검색

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-to-the-new-search-language-automatically"></a>질문: 업그레이드한 작업 영역 외부에 저장된 검색이 있습니다. 이러한 검색을 새 검색 언어로 자동 변환할 수 있나요?
로그 검색 페이지의 언어 변환기 도구를 사용하면 각 검색을 변환할 수 있습니다.  작업 영역을 업그레이드하지 않고 여러 검색을 자동으로 변환하는 방법은 없습니다.

### <a name="question-why-are-my-query-results-not-sorted"></a>질문: 내 쿼리 결과가 정렬되지 않는 이유는 무엇입니까?
새 쿼리 언어에서는 결과가 기본적으로 정렬되지 않습니다.  [정렬 연산자](https://go.microsoft.com/fwlink/?linkid=856079)를 사용하여 하나 이상의 속성으로 결과를 정렬합니다.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>알려진 문제: 목록의 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다
목록의 로그 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다.  업그레이드하기 전에 이러한 속성을 포함할 수 없습니다.  이 문제는 빈 속성은 표시되지 않도록 수정될 예정입니다.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>알려진 문제: 차트에서 값을 선택하면 자세한 결과가 표시되지 않습니다
업그레이드하기 전에 차트에서 값을 선택하면 선택한 값과 일치하는 레코드의 자세한 목록을 반환합니다.  업그레이드 후에 단일 요약된 줄만 반환됩니다.  이 문제는 현재 조사 중입니다.

## <a name="log-search-api"></a>로그 검색 API

### <a name="question-does-the-log-search-api-get-updated-after-i-upgrade"></a>질문: 제가 업그레이드를 수행한 후에 로그 검색 API가 업데이트되었습니까?
[로그 검색 API](log-analytics-log-search-api.md)는 아직 새 검색 언어로 업그레이드되지 않았습니다.  작업 영역을 업그레이드한 후에도 이 API로 레거시 쿼리 언어를 계속 사용합니다.  로그 검색 API가 업데이트되면 업데이트된 해당 설명서를 사용할 수 있게 됩니다.


## <a name="portals"></a>포털

### <a name="question-should-i-use-the-new-advanced-analytics-portal-or-keep-using-the-log-search-portal"></a>질문: 새 고급 분석 포털을 사용해야 합니까? 아니면 로그 검색 포털을 계속 사용해야 합니까?
[Azure Log Analytics에서 로그 쿼리를 만들고 편집하기 위한 포털](log-analytics-log-search-portals.md)에서 두 포털의 비교를 볼 수 있습니다.  각 포털은 분명한 이점이 있으므로 자신의 요구 사항에 가장 적합한 포털을 선택할 수 있습니다.  두 포털 모두 고급 분석 포털에서 쿼리를 작성하고 뷰 디자이너와 같은 다른 위치에 붙여넣을 수 있습니다.  이를 수행할 때 [고려해야 할 문제](log-analytics-log-search-portals.md#advanced-analytics-portal)를 읽어보세요.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>질문: PowerBI 통합에서 변경되는 사항이 있나요?
예.  작업 영역이 업그레이드되면 Log Analytics 데이터를 Power BI로 내보내는 프로세스가 더 이상 작동하지 않습니다.  그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다.  업그레이드 후 Azure Log Analytics는 Application Insights와 같은 플랫폼을 사용하며, [Application Insights 쿼리를 Power BI로 내보내는 프로세스](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)와 같은 프로세스를 사용하여 Log Analytics 쿼리를 Power BI로 내보냅니다.

### <a name="known-issue-power-bi-request-size-limit"></a>알려진 문제: Power BI 요청 크기 제한
현재 Power BI로 내보낼 수 있는 Log Analytics 쿼리에 대한 크기 제한은 8MB입니다.  이 한도는 나중에 상향 조정될 예정입니다.


##<a name="powershell-cmdlets"></a>PowerShell cmdlet

### <a name="question-does-the-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>질문: 제가 업그레이드를 수행한 후에 로그 검색 PowerShell cmdlet이 업데이트되었습니까?
[Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults)는 새 검색 언어로 아직 업그레이드되지 않았습니다.  작업 영역을 업그레이드한 후에도 이 cmdlet으로 레거시 쿼리 언어를 계속 사용합니다.  cmdlet이 업데이트되면 업데이트된 해당 설명서를 사용할 수 있게 됩니다.


## <a name="resource-manager-templates"></a>리소스 관리자 템플릿

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>질문: Resource Manager 템플릿을 사용하여 업그레이드된 작업 영역을 작성할 수 있나요?
예.  2017년 3월 15일 미리 보기의 API 버전을 사용하고 다음 예제와 같이 템플릿의 **기능** 섹션을 포함해야 합니다.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>솔루션

### <a name="question-will-my-solutions-continue-to-work"></a>질문: 내 솔루션이 계속 작동하나요?
모든 솔루션은 업그레이드된 작업 영역에서 계속 작동합니다. 단, 새 쿼리 언어로 변환된 경우 성능은 향상됩니다.  이 섹션에 설명된 일부 기존 솔루션에는 알려진 문제가 있습니다.

### <a name="known-issue-capacity-and-performance-solution"></a>알려진 문제: 용량 및 성능 솔루션
[용량 및 성능](log-analytics-capacity.md) 보기의 일부는 비어 있을 수 있습니다.  이 문제에 대한 수정은 곧 사용할 수 있습니다.

### <a name="known-issue-device-health-solution"></a>알려진 문제: 장치 상태 솔루션
[장치 상태 솔루션](https://docs.microsoft.com/windows/deployment/update/device-health-monitor)은 업그레이드된 작업 영역의 데이터를 수집하지 않습니다.  이 문제에 대한 수정은 곧 사용할 수 있습니다.

### <a name="known-issue-application-insights-connector"></a>알려진 문제: Application Insights 커넥터
[Application Insights 커넥터 솔루션](log-analytics-app-insights-connector.md)의 관점은 현재 업그레이드된 작업 영역에서 지원되지 않습니다.  이 문제에 대한 수정은 현재 분석 중입니다.

## <a name="upgrade-process"></a>업그레이드 프로세스

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-the-same-time"></a>질문: 작업 영역이 여러 개 있습니다. 모든 작업 영역을 동시에 업그레이드할 수 있나요?  
아니요.  각 업그레이드는 단일 작업 영역에 적용됩니다. 현재는 여러 작업 영역을 한 번에 업그레이드할 수 있는 방법이 없습니다. 업그레이드된 작업 영역의 다른 사용자도 영향을 받게 됩니다.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>질문: 업그레이드하면 작업 영역에 수집되어 있는 기존 로그 데이터가 수정되나요?  
아니요. 작업 영역 검색에 사용할 수 있는 로그 데이터는 업그레이드의 영향을 받지 않습니다. 저장된 검색, 경고 및 보기는 새 검색 언어로 자동 변환됩니다.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>질문: 내 작업 영역을 업그레이드하지 않으면 어떻게 되나요?  
향후 몇 개월 이내에 레거시 로그 검색은 사용되지 않을 예정입니다. 이 시점까지 업그레이드하지 않은 작업 영역은 자동으로 업그레이드됩니다.

### <a name="question-i-didnt-choose-to-upgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>질문: 업그레이드를 선택하지 않았는데도 내 작업 영역이 업그레이드되었습니다! 어떻게 된 건가요?  
해당 작업 영역의 다른 관리자의 작업 영역을 업그레이드했을 수 있습니다. 새 언어가 일반 공급 상태가 되면 모든 작업 영역은 자동으로 업그레이드됩니다.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-to-cancel-it-and-restore-everything-back-what-should-i-do"></a>질문: 실수로 업그레이드를 해서 취소하고 모든 항목을 다시 복원해야 합니다. 어떻게 해야 하나요?  
걱정하실 필요가 없습니다.  업그레이드 전에 작업 영역의 스냅숏이 생성되었으므로 해당 스냅숏을 복원하면 됩니다. 하지만 업그레이드 후에 저장한 검색, 경고 또는 보기는 손실됩니다.  작업 영역 환경을 복원하려면 [업그레이드 후에 다시 원래대로 되돌릴 수 있나요?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)의 절차를 따르세요.


## <a name="views"></a>뷰

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>질문: 뷰 디자이너를 통해 새 뷰를 만들려면 어떻게 할까요?
업그레이드하기 전에 주 대시보드의 타일에서 뷰 디자이너로 새 뷰를 만들 수 있습니다.  작업 영역이 업그레이드되면 이 타일은 제거됩니다.  왼쪽 메뉴의 녹색 + 단추를 클릭하여 OMS 포털에서 뷰 디자이너로 새 뷰를 만들 수 있습니다.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>알려진 문제: 뷰에서 꺾은선형 차트에 대한 모두 보기 옵션을 사용해도 꺾은선형 차트로 결과가 표시되지 않습니다.
뷰의 꺾은선형 차트에서 아래쪽에 *모두 보기*옵션을 클릭하면 테이블이 표시됩니다.  업그레이드하기 전에는 꺾은선형 차트로 표시됩니다.  이 문제는 잠재적 수정에 대한 분석 중입니다.


## <a name="next-steps"></a>다음 단계

- [새 Log Analytics 쿼리 언어로 작업 영역 업그레이드](log-analytics-log-search-upgrade.md)에 대해 자세히 알아봅니다.

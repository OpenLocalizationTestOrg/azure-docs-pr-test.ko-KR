---
title: "aaaLog 분석 새 로그 검색에 대 한 질문과 대답 | Microsoft Docs"
description: "이 문서에서는 로그 분석 toohello 새로운 쿼리 언어의 hello 업그레이드와 관련 한 질문과 대답을 제공 합니다."
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
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Log Analytics 새 로그 검색 FAQ 및 알려진 문제

이 문서에서는의 hello 업그레이드와 관련 한 알려진된 문제 및 질문과 대답 [로그 분석 toohello 새로운 쿼리 언어](log-analytics-log-search-upgrade.md)합니다.  작업 영역 hello 의사 결정 tooupgrade 하기 전에이 전체 문서를 통해 읽어야 합니다.


## <a name="alerts"></a>경고

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>질문: 경고 규칙이 매우 많습니다. Toocreate 필요 한가요 hello 새로운 언어 업그레이드 후에서 다시 해당?  
아니요, 경고 규칙에는 업그레이드 하는 동안 자동으로 변환 된 toohello 새 검색 언어입니다.  


## <a name="computer-groups"></a>컴퓨터 그룹

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>질문: 오류가 발생 때 toouse 컴퓨터 그룹입니다.  구문이 변경되었나요?
예, 컴퓨터를 사용 하기 위한 hello 구문을 작업 영역 업그레이드 될 때 변경 내용 그룹화 합니다.  자세한 내용은 [Log Analytics 로그 검색의 컴퓨터 그룹](log-analytics-computer-groups.md)을 참조하세요.

### <a name="known-issue-groups-imported-from-active-directory"></a>알려진 문제: Active Directory에서 가져온 그룹
현재 Active Directory에서 가져온 컴퓨터 그룹을 사용하는 쿼리를 만들 수 없습니다.  문제를 해결 하려면이 문제를 해결할 때까지 가져온 hello Active Directory 그룹을 사용 하 여 새 컴퓨터 그룹 만들고 쿼리에 해당 새 그룹을 사용 합니다.

예제 쿼리 toocreate 가져온된 Active Directory 그룹을 포함 하는 새 컴퓨터 그룹은 다음과 같습니다.

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>대시보드

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>질문: 대시보드를 업그레이드된 작업 영역에서 계속 사용할 수 있나요?
Toouse 너무 추가한 모든 타일을 계속할 수**내 대시보드** 작업 영역, 업그레이드 되지만 해당 타일을 편집 하거나 새로 추가할 수 없습니다.  Toocreate 계속 하 고 사용 하 여 뷰를 편집할 수 [뷰 디자이너](log-analytics-view-designer.md) hello Azure 포털의에서 대시보드를 만들 수도 있습니다.


## <a name="log-searches"></a>로그 검색

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>질문: 업그레이드한 작업 영역 외부에 저장된 검색이 있습니다. 변환할 수으로 새 검색 언어 toohello 자동으로
각 로그 검색 페이지 tooconvert hello에에서 hello 언어 변환기 도구를 사용할 수 있습니다.  Hello 작업 영역을 업그레이드 하지 않고 여러 개의 검색 메서드 tooautomatically 변환 되지 않습니다.

### <a name="question-why-are-my-query-results-not-sorted"></a>질문: 내 쿼리 결과가 정렬되지 않는 이유는 무엇입니까?
Hello 새로운 쿼리 언어에서 기본적으로 결과 정렬 되지 않습니다.  사용 하 여 hello [sort 연산자](https://go.microsoft.com/fwlink/?linkid=856079) toosort 하나 이상의 속성을 기준으로 결과입니다.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>알려진 문제: 목록의 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다
목록의 로그 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다.  이전 tooupgrade 이러한 속성은 포함할 수 없습니다.  이 문제는 빈 속성은 표시되지 않도록 수정될 예정입니다.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>알려진 문제: 차트에서 값을 선택하면 자세한 결과가 표시되지 않습니다
이전 tooupgrade 차트에서 값을 선택 하면 선택한 hello 값과 일치 하는 레코드의 자세한 목록을 반환 됩니다.  업그레이드 후 hello 단일 요약 된 줄만 반환 됩니다.  이 문제는 현재 조사 중입니다.

## <a name="log-search-api"></a>로그 검색 API

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>질문: hello 로그 검색 API 업데이트지 않습니다 업그레이드 하나요?
hello [로그 검색 API](log-analytics-log-search-api.md) 아직 업그레이드 toohello 새 검색 언어를 되지 않았습니다.  작업 영역을 업그레이드 한 후에이 api를 toouse hello 레거시 쿼리 언어를 계속 합니다.  업데이트 될 때 업데이트 된 설명서 hello 로그 검색 API에 대해 사용할 수 있습니다.


## <a name="portals"></a>포털

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>질문: hello 새 Advanced Analytics 포털을 사용 하거나 해야 hello 로그 검색 포털을 사용 하 여 유지?
hello 두 포털의 비교를 볼 수 있습니다 [만들고 Azure 로그 분석에서 로그 쿼리를 편집 하기 위한 포털](log-analytics-log-search-portals.md)합니다.  각 분명 한 이점이 요구 사항에 가장 적합 한 hello를 선택할 수 있습니다.  Hello Advanced Analytics 포털에서 일반적인 toowrite 쿼리 이며 뷰 디자이너 같은 다른 위치에 붙여 넣습니다.  읽어야 할 [tooconsider 발급](log-analytics-log-search-portals.md#advanced-analytics-portal) 수행할 때입니다.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>질문: PowerBI 통합에서 변경되는 사항이 있나요?
예.  작업 영역이 업그레이드 되 면 다음 hello 로그 분석 데이터 tooPower BI를 내보내기 위한 더 이상 사용할 수 없습니다.  그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다.  업그레이드 후 Azure 로그 분석 사용 하 여 hello Application Insights와 같은 플랫폼 및 동일한 프로세스으로 tooexport 로그 분석 쿼리 tooPower BI hello를 사용 하 여 [hello 프로세스 tooexport Application Insights 쿼리 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)합니다.

### <a name="known-issue-power-bi-request-size-limit"></a>알려진 문제: Power BI 요청 크기 제한
현재 내보낸된 tooPower BI 일 수 있는 로그 분석 쿼리에 대 한 8MB의 크기 제한이 됩니다.  이 한도는 나중에 상향 조정될 예정입니다.


##<a name="powershell-cmdlets"></a>PowerShell cmdlet

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>질문: hello 로그 검색 PowerShell cmdlet 업데이트지 않습니다 업그레이드 하나요?
hello [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) 아직 업그레이드 toohello 새 검색 언어를 되지 않았습니다.  작업 영역을 업그레이드 한 후에이 cmdlet과 toouse hello 레거시 쿼리 언어를 계속 합니다.  업데이트 될 때 업데이트 된 설명서 hello cmdlet에 대 한 사용할 수 있습니다.


## <a name="resource-manager-templates"></a>리소스 관리자 템플릿

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>질문: Resource Manager 템플릿을 사용하여 업그레이드된 작업 영역을 작성할 수 있나요?
예.  2017-03-15-미리 보기의 API 버전을 사용 하 고 포함 해야는 **기능** hello 다음 예제와 같이 서식 파일의 섹션입니다.

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

### <a name="question-will-my-solutions-continue-toowork"></a>질문: 계속 됩니다. 내 솔루션 toowork
모든 솔루션은 계속 toowork 된 업그레이드 된 작업 영역에서 변환 된 toohello 새로운 쿼리 언어는 경우 성능을 향상 됩니다.  이 섹션에 설명된 일부 기존 솔루션에는 알려진 문제가 있습니다.

### <a name="known-issue-capacity-and-performance-solution"></a>알려진 문제: 용량 및 성능 솔루션
Hello에 있는 hello 부분의 일부 [용량 및 성능](log-analytics-capacity.md) 보기 비어 있을 수 있습니다.  수정 프로그램 toothis 문제를 곧 사용할 수 있습니다.

### <a name="known-issue-device-health-solution"></a>알려진 문제: 장치 상태 솔루션
hello [장치 상태 솔루션](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) 는 업그레이드 된 작업 영역 데이터를 수집 하지 것입니다.  수정 프로그램 toothis 문제를 곧 사용할 수 있습니다.

### <a name="known-issue-application-insights-connector"></a>알려진 문제: Application Insights 커넥터
[Application Insights 커넥터 솔루션](log-analytics-app-insights-connector.md)의 관점은 현재 업그레이드된 작업 영역에서 지원되지 않습니다.  수정 프로그램 toothis 문제는 현재 분석입니다.

## <a name="upgrade-process"></a>업그레이드 프로세스

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>질문: 작업 영역이 여러 개 있습니다. 업그레이드 하는 hello에서 모든 작업 영역 동시?  
아니요.  업그레이드 될 때마다 tooa 단일 작업 영역에 적용 됩니다. 현재는 여러 작업 영역을 한 번에 업그레이드할 수 있는 방법이 없습니다. 하십시오 참고 작업 영역을 업그레이드 하는 hello의 다른 사용자도 적용 됩니다.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>질문: 업그레이드하면 작업 영역에 수집되어 있는 기존 로그 데이터가 수정되나요?  
아니요. hello 로그 데이터를 사용할 수 있는 tooyour 작업 영역 검색 hello 업그레이드에 의해 영향을 받지 않습니다. 저장 된 검색, 경고 및 보기 변환된 toohello 새 검색 언어에 자동으로 지워집니다.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>질문: 내 작업 영역을 업그레이드하지 않으면 어떻게 되나요?  
hello 레거시 로그 검색 월 들어오는 hello에서 제외 될 예정입니다. 이 시점까지 업그레이드하지 않은 작업 영역은 자동으로 업그레이드됩니다.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>질문: tooupgrade, 선택 하지 않은 있지만 내 작업 영역 그래도 업그레이드 되었습니다! 어떻게 된 건가요?  
이 작업 영역의 다른 관리자 hello 작업 영역을 업그레이드 있을 수 있습니다. Hello 새 언어에 일반 공급 하는 경우 작업 영역을 모두 자동으로 업그레이드 되지 됩니다 note 하십시오.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>질문: 실수로 업그레이드 했으며 및 모든 내용을 복원 toocancel 필요 합니다. 어떻게 해야 하나요?  
걱정하실 필요가 없습니다.  업그레이드 전에 작업 영역의 스냅숏이 생성되었으므로 해당 스냅숏을 복원하면 됩니다. 검색, 경고 또는 hello 업그레이드 하지만 손실 됩니다 후 저장 보기 염두에서에 둬야 합니다.  toorestore에 hello 절차에 따라 작업 영역 환경의 [업그레이드 후에 다시 이동 수 있습니까?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>뷰

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>질문: 뷰 디자이너를 통해 새 뷰를 만들려면 어떻게 할까요?
이전 tooupgrade hello 주 대시보드의 타일에서 새 뷰를 뷰 디자이너를 만들 수 있습니다.  작업 영역이 업그레이드되면 이 타일은 제거됩니다.  안녕하세요 녹색 + hello 왼쪽된 메뉴의 단추를 클릭 하 여 hello OMS 포털에서 보기 디자이너로 새 뷰를 만들 수 있습니다.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>알려진 문제: 뷰에서 꺾은선형 차트에 대한 모두 보기 옵션을 사용해도 꺾은선형 차트로 결과가 표시되지 않습니다.
Hello에 클릭할 때 *스크롤하게* 옵션 보기에는 꺾은선형 차트 파트의 hello 맨 아래에 표시 되는 테이블입니다.  이전 tooupgrade 꺾은선형 차트와 함께 제공 된 것입니다.  이 문제는 잠재적 수정에 대한 분석 중입니다.


## <a name="next-steps"></a>다음 단계

- 에 대 한 자세한 내용은 [작업 영역 toohello 업그레이드 새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md)합니다.

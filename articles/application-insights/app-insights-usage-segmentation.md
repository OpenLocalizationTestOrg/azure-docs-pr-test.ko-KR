---
title: "Azure Application Insights에서 aaaUser, 세션 및 이벤트 분석 | Microsoft docs"
description: "웹앱의 사용자 인구 통계 분석입니다."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Application Insights의 사용자, 세션 및 이벤트 분석

사람들이 사용자의 웹앱을 사용하는 경우, 가장 큰 관심을 갖는 페이지, 사용자가 있는 위치 및 사용하는 브라우저 및 운영 체제를 알아봅니다. [Azure Application Insights](app-insights-overview.md)를 사용하여 업무 및 원격 사용을 분석합니다.

## <a name="get-started"></a>시작

Hello 사용자, 세션 또는 이벤트 블레이드 hello Application Insights 포털에서에서 데이터를 아직 표시 되지 않으면 [tooget hello 사용량 도구를 시작 하는 방법에 대해 알아봅니다](app-insights-usage-overview.md)합니다.

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>hello 사용자, 세션 및 이벤트 조각화 도구

동일한 도구 tooslice 분리 및 분할에서에서 원격 분석 세 가지 관점에서 웹 응용 프로그램을 hello 블레이드를 사용 하는 hello 사용 중 3 개. 를 필터링 및 hello 데이터 분할 hello 상대 사용의 다른 페이지 및 기능에 대 한 통찰력을 열 수 있습니다.

* **사용자 도구**: 사용자의 앱 및 해당 기능을 사용한 사람의 수.  사용자 수는 브라우저 쿠키에 저장되는 익명 ID를 사용하여 계산합니다. 여러 브라우저 또는 컴퓨터를 사용하는 한 사람은 둘 이상의 사용자로 계산됩니다.
* **세션 도구**: 앱의 특정 페이지 및 기능을 포함하는 사용자 활동 세션의 수. 사용자의 비활동 상태가 30분 경과된 이후 또는 연속해서 24시간 사용한 후에 세션 수가 계산됩니다.
* **이벤트 도구**: 앱의 특정 페이지 및 기능이 사용되는 빈도. 사용자가 [앱을 계측](app-insights-javascript.md)한 경우 페이지 보기 횟수는 브라우저가 앱에서 페이지를 로드할 때 계산됩니다. 

    사용자 지정 이벤트는 주로 사용자 상호 작용 하는 단추를 클릭 하거나 일부 작업의 완료를 hello와 같은 응용 프로그램에서 발생 하는 것에 대 한 항목을 나타냅니다. 코드에에서 삽입할 앱 너무[사용자 지정 이벤트를 생성](app-insights-api-custom-events-metrics.md#trackevent)합니다.

![사용 도구](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>특정 사용자에 대해 쿼리 

Hello 위쪽 hello 사용자 도구에 hello 쿼리 옵션을 조정 하 여 서로 다른 사용자 그룹을 탐색 합니다. 

* 사용한 사람: 사용자 지정 이벤트 및 페이지 보기를 선택합니다. 
* 기간: 시간 범위를 선택합니다. 
* : 하 여 일정 시간 동안 또는 브라우저 또는 도시와 같은 다른 속성 데이터를 toobucket hello 하는 방법을 선택 합니다. 
* 분할에: toosplit 또는 세그먼트 hello 데이터 속성을 선택 합니다. 
* 필터 추가: hello 쿼리 toocertain 사용자, 세션 또는 브라우저 또는 도시 등의 속성을 기준으로 이벤트를 제한 합니다. 
 
## <a name="saving-and-sharing-reports"></a>보고서 저장 및 공유 
Hello 공유 보고서 섹션의에서 모든 액세스 toothis Application Insights 리소스를 가진 다른 사용자와 공유 하거나 hello 내 보고서 섹션의 두 개인 정당한 tooyou, 사용자가 보고서를 저장할 수 있습니다.  
 
보고서 저장 또는 속성을 편집 하는 동안 보고서는 지속적으로 "현재 상대 시간 범위" toosave 시간의 일부 고정된 크기를 다시 살펴보자면, 데이터 새로 고침을 선택 합니다.  
 
"현재 절대 시간 범위" toosave 고정된 데이터 집합을 사용 하 여 보고서를 선택 합니다. Application Insights에서 데이터는 90 일 이상 된 절대 시간 범위를 사용 하 여 보고서 이후 경과한 경우 저장 하므로 90 일 동안만 저장 점을 염두에 hello 보고서를 빈 상태로 표시 됩니다. 
 
## <a name="example-instances"></a>예제 인스턴스

hello 인스턴스 "예" 섹션에서는 몇 가지 개별 사용자, 세션 또는 hello 현재 쿼리를 통해 일치 하는 이벤트에 대 한 정보를 보여 줍니다. 또한 tooaggregates에서 개인의 hello 동작 하는 방법과 고려 실제로 사용자 응용 프로그램의 사용 방법에 대 한 통찰력을 제공할 수 있습니다. 
 
## <a name="insights"></a>자세한 정보 

hello Insights 사이드바 공용 속성을 공유 하는 사용자의 큰 클러스터를 보여 줍니다. 이러한 클러스터는 사람들이 사용자의 앱을 사용하는 방식에 대한 놀라운 추세를 보여 줄 수 있습니다. 예를 들어, 모든 응용 프로그램의 hello 사용의 40%는 하나의 기능을 사용 하는 사용자에서 제공 합니다.  


## <a name="next-steps"></a>다음 단계
- tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.
- 사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.
    - [깔때기](usage-funnels.md)
    - [보존](app-insights-usage-retention.md)
    - [사용자 흐름](app-insights-usage-flows.md)
    - [통합 문서](app-insights-usage-workbooks.md)
    - [사용자 컨텍스트 추가](app-insights-usage-send-user-context.md)


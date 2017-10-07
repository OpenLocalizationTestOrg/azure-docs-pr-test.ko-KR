---
title: "논리 앱에 대 한 통찰력을 aaaMonitor 및 get OMS-Azure 논리 앱을 사용 하 여 실행 | Microsoft Docs"
description: "논리 응용 프로그램이 실행 되 로그 분석 및 Operations Management Suite (OMS) tooget insights 및 문제 해결 및 진단에 대 한 보다 풍부한 디버깅 세부 정보로 모니터링"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>OMS(Operations Management Suite) 및 Log Analytics를 사용한 논리 앱 실행에 관한 모니터링 및 정보 활용

모니터링 및 다양 한 디버깅 정보에 대 한 켤 수 있습니다 로그 분석 hello에서 논리 앱을 만들 때 동시 합니다. 로그 분석 hello Operations Management Suite (OMS) 포털을 통해 실행 되는 진단 로깅 및 논리 앱에 대 한 모니터링을 제공 합니다. 논리 앱 관리 솔루션 tooOMS hello를 추가한 경우에 논리가 응용 프로그램 실행 및 상태, 실행 시간, 다시 전송 상태 및 상관 관계 Id와 같은 특정 세부 정보에 대 한 집계 된 상태를 가져옵니다.

이 항목에서는 런타임 이벤트를 볼 수 있으며 논리 앱에 대 한 데이터를 실행 하므로 OMS에서 논리 앱 관리 솔루션 hello tooturn 로그 분석 또는 설치에는 방법을 보여 줍니다.

 > [!TIP]
 > toomonitor 기존 논리 앱이 너무 다음이 단계를 수행 [진단 로깅을 켜고 논리가 응용 프로그램 런타임 데이터 tooOMS 보낼](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.

## <a name="requirements"></a>요구 사항

시작 하기 전에 toohave OMS 작업 영역 해야 합니다. 자세한 내용은 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다. 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>논리 앱을 만들 때 진단 로깅 켜기

1. [Azure Portal](https://portal.azure.com)에서 논리 앱을 만듭니다. **새로 만들기** > **엔터프라이즈 통합** > **논리 앱** > **만들기**를 선택합니다.

   ![논리 앱 만들기](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Hello에 **만들기 논리 앱** 페이지에서 표시 된 것 처럼 이러한 작업을 수행 합니다.

   1. 논리 앱의 이름을 입력하고 Azure 구독을 선택합니다. 
   2. Azure 리소스 그룹을 만들거나 선택합니다.
   3. 설정 **로그 분석** 너무**에**합니다. 
   너무 논리 앱에 대 한 데이터를 전송 하려는 선택 hello OMS 작업 영역을 실행 합니다. 
   4. 준비 되 면 선택 **Pin toodashboard** > **만들기**합니다.

      ![논리 앱 만들기](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      이 단계를 마치면 Azure에서 OMS 작업 영역에 연결된 논리 앱이 만들어집니다. 
      또한이 단계는 자동으로 OMS 작업 영역에서 hello 논리 앱 관리 솔루션을 설치합니다.

3. OMS에서 논리 앱이 실행 tooview [다음이 단계를 계속](#view-logic-app-runs-oms)합니다.

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>OMS의 hello 논리 앱 관리 솔루션을 설치 합니다.

사용자의 논리 앱을 만들 때 이미 Log Analytics를 켰으면 이 단계를 건너뜁니다. Hello 논리 앱 관리 솔루션을 OMS에 설치 된 이미 있습니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다. 필터로 “로그 분석”을 검색하고 다음과 같이 **Log Analytics**를 선택합니다.

   !["Log Analytics" 선택](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. **Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다. 

   ![OMS 작업 영역 선택](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. **관리** 아래에서 **OMS 포털**을 선택합니다.

   !["OMS 포털" 선택](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. OMS 홈 페이지에 업그레이드 배너 hello 나타나면 선택 hello 배너 OMS 작업 영역을 먼저 업그레이드 합니다. 그런 다음 **솔루션 갤러리**를 선택합니다.

   ![“솔루션 갤러리” 선택](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. 아래 **모든 솔루션**찾아 hello에 대 한 hello 타일 선택 **논리 앱 관리** 솔루션입니다.

   ![“논리 앱 관리” 선택](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. OMS 작업 영역에서 tooinstall hello 솔루션 선택 **추가**합니다.

   ![“논리 앱 관리”에 “추가” 선택](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>OMS 작업 영역에서 논리 앱 실행 보기

1. tooview hello 개수 및 논리 앱에 대 한 상태 실행 되므로 OMS 작업 영역에 대 한 이동 toohello 개요 페이지. Hello에 hello 세부 정보를 검토 **논리 앱 관리** 바둑판식으로 배열입니다.

   ![논리 앱 실행 횟수 및 상태를 보여 주는 개요 타일](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > 이 업그레이드 배너 hello 논리 앱 관리 타일 대신 나타나면, OMS 작업 영역을 먼저 업그레이드 hello 배너를 선택 합니다.
  
   > !["OMS 작업 영역" 업그레이드](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. 프로그램 논리를 응용 프로그램 실행에 대 한 자세한 정보는 요약 tooview hello 선택 **논리 앱 관리** 바둑판식으로 배열입니다.

   여기에서 논리 앱 실행은 이름이나 실행 상태로 그룹화됩니다.

   ![논리 앱 실행에 대한 상태 요약](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. 특정 논리 앱 또는 상태, 논리 앱 또는 상태에 대 한 선택 hello 행에 대 한 모든 hello tooview 실행 됩니다.

   특정 논리 앱에 대 한 모든 hello 실행을 보여 주는 예제는 다음과 같습니다.

   ![논리 앱 또는 상태에 대한 실행 보기](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > hello **다시 전송** 열 다시 제출 된 실행에서 발생 하는 실행에 대 한 "예"를 표시 합니다.

4. 이러한 결과 toofilter, 클라이언트와 서버 쪽 필터링을 수행할 수 있습니다.

   * 클라이언트 쪽 필터: 각 열에 대해 원하는 hello 필터를 선택 합니다. 
   다음은 몇 가지 예입니다.

     ![예제 열 필터](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * 서버 쪽 필터: toochoose 실행 hello hello 페이지 위쪽에 hello 범위 컨트롤을 사용 하 여 표시 되는 특정 시간 창 또는 toolimit hello 수 있습니다. 
   기본적으로 1,000개 레코드가 한 번에 나타납니다. 
   
     ![변경 hello 시간 창](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. 모든 tooview hello 로그 검색 페이지를 열고 행 작업 및 특정 실행된을 선택 하기 위한 세부 정보 hello 합니다. 

   * tooview이이 정보는 테이블의 선택 **테이블**합니다.
   * toochange hello 쿼리 hello 검색 창에 쿼리 문자열 hello를 편집할 수 있습니다. 
   향상된 경험을 위해 **고급 분석**을 선택합니다.

     ![논리 앱 실행에 대한 작업 및 세부 정보 보기](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     여기 hello Azure 로그 분석 페이지에서 업데이트할 수 있습니다 쿼리 및 뷰 hello hello 테이블에서 발생 합니다. 
     이 쿼리에서 사용 하 여 [Kusto 쿼리 언어](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), tooview 다른 결과 편집할 수 있는 합니다. 

     ![Azure Log Analytics - 쿼리 뷰](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>다음 단계

* [B2B 메시지 모니터링](../logic-apps/logic-apps-monitor-b2b-message.md)

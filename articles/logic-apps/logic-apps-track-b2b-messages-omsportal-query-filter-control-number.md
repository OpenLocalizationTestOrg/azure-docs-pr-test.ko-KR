---
title: "Operations Management Suite-Azure 논리 앱에서에서 B2B 메시지에 대 한 aaaQuery | Microsoft Docs"
description: "Hello Operations Management Suite에서에서 쿼리 tootrack AS2, x12 및 EDIFACT 메시지 만들기"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>X12 및 EDIFACT 메시지 hello Microsoft Operations Management Suite (OMS)에서 a s 2에 대 한 쿼리

x12 또는 EDIFACT 메시지를 추적 하 고 있는 toofind hello AS2 [Azure 로그 분석](../log-analytics/log-analytics-overview.md) hello에 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), 특정에 따라 작업을 필터링 하는 쿼리를 만들 수 있습니다 조건입니다. 예를 들어 특정 교환 컨트롤 번호에 따라 메시지를 찾을 수 있습니다.

## <a name="requirements"></a>요구 사항

* 진단 로깅과 함께 설정된 논리 앱. 자세한 내용은 [어떻게 toocreate 논리 앱](../logic-apps/logic-apps-create-a-logic-app.md) 및 [어떻게 tooset 해당 논리 앱에 대 한 로깅을](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.

* 모니터링 및 로깅을 사용하여 설정된 통합 계정. 자세한 [어떻게 toocreate 통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) 및 [방법을 모니터링 해당 계정에 대 한 로깅을 켜고 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)합니다.

* 아직 없는 경우, [진단 데이터 tooLog 분석 게시](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) 및 [OMS에서 메시지 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.

> [!NOTE]
> Hello에 대 한 작업 영역 있어야 hello 이전 요구 사항을 충족 한 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다. 사용 해야 hello OMS에서이 프로그램 B2B 통신을 추적 하기 위한 동일한 OMS 작업 영역입니다. 
>  
> OMS 작업 영역에 없을 경우에 대해 배울 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Hello Operations Management Suite 포털에서 필터로 메시지 쿼리 만들기

이 예제는 해당 교환 컨트롤 번호에 따라 메시지를 찾는 방법을 보여 줍니다.

> [!TIP] 
> OMS 작업 영역 이름을 알고 있는 경우 이동 tooyour 작업 영역 홈 페이지 (`https://{your-workspace-name}.portal.mms.microsoft.com`), 4 단계에서 시작 합니다. 그렇지 않은 경우 1단계에서 시작합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다. "로그 분석"에 대해 검색한 후 다음과 같이 **Log Analytics**를 선택합니다.

   ![Log Analytics 찾기](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. **Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.

   ![OMS 작업 영역 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. **관리** 아래에서 **OMS 포털**을 선택합니다.

   ![OMS 포털 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. OMS 홈페이지에서 **로그 검색**을 선택합니다.

   ![OMS 홈페이지에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   또는

   ![Hello OMS 메뉴에서 "로그 검색"를 선택 합니다.](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Hello 검색 상자에 원하는 toofind, 필드를 입력 한 키를 누릅니다 **Enter**합니다. 입력을 시작할 때 OMS는 사용할 수 있는 가능한 일치 및 작업을 보여 줍니다. 에 대 한 자세한 내용은 [어떻게 로그 분석의 데이터를 toofind](../log-analytics/log-analytics-log-searches.md)합니다.

   이 예제에서는 **Type=AzureDiagnostics**로 이벤트를 검색합니다.

   ![쿼리 문자열 입력 시작](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Hello 왼쪽된 모음에서 hello 시간 범위 선택 tooview 되도록 합니다. tooadd 필터 tooyour 쿼리 선택 **+ 추가**합니다.

   ![필터 tooquery 추가](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. 아래 **필터 추가**, 원하는 hello 필터를 찾을 수 있도록 hello 필터 이름을 입력 합니다. Hello 필터를 선택 하 고 선택 **+ 추가**합니다.

   toofind hello 교환 컨트롤 번호,이 예에서는 "교환" hello 단어를 검색 한 선택 **event_record_messageProperties_interchangeControlNumber_s** hello 필터로 합니다.

   ![필터 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Hello 왼쪽된 모음에서 toouse, 원하고 선택 hello 필터 값 선택 **적용**합니다.

   이 예에서는 원하는 hello 메시지에 대 한 hello 교환 컨트롤 번호를 선택 합니다.

   ![필터 값 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. 이제 만든다면 toohello 쿼리를 반환 합니다. 선택한 필터 이벤트 및 값으로 쿼리가 업데이트되었습니다. 이제 이전 결과 또한 필터링되어 있습니다.

    ![필터링 결과 tooyour 쿼리를 반환 합니다.](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>나중에 사용할 쿼리 저장

1. Hello에 쿼리에서 **로그 검색** 페이지에서 선택 **저장**합니다. 쿼리에 이름을 지정하고 범주를 선택하고 **저장**을 선택합니다.

   ![쿼리에 이름 및 범주 지정](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview 쿼리에 선택 **즐겨찾기**합니다.

   !["즐겨찾기" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. 아래 **저장 된 검색**를 hello 결과 볼 수 있도록 쿼리를 선택 합니다. 서로 다른 결과 찾을 수 있도록 tooupdate hello 쿼리 hello 쿼리를 편집 합니다.

   ![쿼리 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>찾기 및 hello Operations Management Suite 포털에 저장 된 쿼리를 실행 합니다.

1. OMS 작업 영역 홈페이지(`https://{your-workspace-name}.portal.mms.microsoft.com`)를 열고 **로그 검색**을 선택합니다.

   ![OMS 홈페이지에서 "로그 검색" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   또는

   ![Hello OMS 메뉴에서 "로그 검색"를 선택 합니다.](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Hello에 **로그 검색** 홈 페이지에서 선택 **즐겨찾기**합니다.

   !["즐겨찾기" 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. 아래 **저장 된 검색**를 hello 결과 볼 수 있도록 쿼리를 선택 합니다. 서로 다른 결과 찾을 수 있도록 tooupdate hello 쿼리 hello 쿼리를 편집 합니다.

   ![쿼리 선택](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>다음 단계

* [AS2 추적 스키마](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 추적 스키마](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [사용자 지정 추적 스키마](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)
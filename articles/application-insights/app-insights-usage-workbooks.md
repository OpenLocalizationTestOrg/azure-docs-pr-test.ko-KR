---
title: "Azure Application Insights의 대화형 통합 문서와 aaaInvestigate 및 공유 사용 현황 데이터 | Microsoft docs"
description: "웹앱의 사용자 인구 통계 분석입니다."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Application Insights에서 대화형 통합 문서를 사용하여 사용 현황 데이터 조사 및 공유

통합 문서는 [Azure Application Insights](app-insights-overview.md) 데이터 시각화, [분석 쿼리](app-insights-analytics.md) 및 텍스트를 대화형 문서로 결합합니다. 통합 문서는 편집 가능한 다른 팀 멤버가 액세스 toohello와 같은 Azure 리소스입니다. 즉, hello 쿼리와 컨트롤 사용 되는 toocreate 통합 문서는 쉽게 tooexplore 있도록 hello 통합 문서를 읽는 사용 가능한 tooother 사용자, 확장 및 실수를 확인 합니다.

통합 문서는 다음과 같은 시나리오에 유용합니다.

* 응용 프로그램의 hello 사용을 탐색 하 여 관심 있는 메트릭 hello를 사전에 모르는 경우: 사용자, 보존 율이 높아지고, 변환율 등의 숫자입니다. Application Insights의 다른 사용 현황 분석 도구와는 달리 통합 문서를 통해 이러한 종류의 자유 형식 탐색에 매우 유용하도록 여러 종류의 시각화 및 분석을 결합할 수 있습니다.
* Tooyour 팀 새로 릴리스된 기능 수행 되는 방법을 설명 하는, 보여 주는 사용자에 의해 계산 키 상호 작용 및 기타 수치에 대 한 합니다.
* 공유는 A의 hello 결과 팀의 다른 멤버와 응용 프로그램에서 실험 B /입니다. Hello에 대 한 hello 목표 텍스트를 사용해 다음 각 사용량 메트릭을 표시 하 고 각 메트릭에 위 또는 아래-대상 했는지 여부에 대 한 지우기 설명선 함께 tooevaluate hello 실험을 사용 하는 분석 쿼리를 설명할 수 있습니다.
* 응용 프로그램 데이터, 텍스트 설명과 hello 앞에 다음 단계 tooprevent 중단에 대 한 내용은 결합의 hello 사용에 중단의 영향 hello를 보고 합니다.

> [!NOTE]
> Application Insights 리소스 페이지 뷰 또는 사용자 지정 이벤트 toouse 통합 문서에 포함 해야 합니다. [Tooset 앱 toocollect 페이지를 자동으로 hello Application Insights JavaScript SDK로 보는 방법에 대해 알아봅니다](app-insights-javascript.md)합니다.
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>통합 문서 섹션 편집, 다시 정렬, 복제 및 삭제

통합 문서는 개별 편집 가능한 사용 현황 시각화, 차트, 테이블, 텍스트 또는 분석 쿼리 결과의 섹션으로 구성됩니다.

통합 문서 섹션의 tooedit hello 내용을 클릭 hello **편집** 아래 단추 및 toohello hello 통합 문서 섹션의 오른쪽입니다.

![Application Insights 통합 문서 섹션 편집 컨트롤](./media/app-insights-usage-workbooks/editing-controls.png)

1. 완료 하면 클릭 섹션을 편집 **편집 수행** hello 하단 왼쪽된 모서리 hello 섹션에에서 있습니다.

2. 섹션의 중복 toocreate 클릭 hello **이 섹션을 복제할** 아이콘입니다. 중복 된 섹션을 만들기 이전 반복을 손실 하지 않고 쿼리에 훌륭한 tooway tooiterate입니다.

3. 통합 문서에서 섹션 toomove 클릭 hello **위로 이동** 또는 **아래로 이동** 아이콘입니다.

4. 영구적으로 클릭 하 여 hello tooremove 섹션 **제거** 아이콘입니다.

## <a name="adding-usage-data-visualization-sections"></a>사용 현황 데이터 시각화 섹션 추가

통합 문서는 네 가지 유형의 기본 제공 사용 현황 분석 시각화를 제공합니다. 각 응용 프로그램의 hello 사용에 대 한 일반적인 질문에 응답합니다. tooadd 테이블 및 차트 이러한 4 개의 섹션 이외의 분석 쿼리 섹션 (아래 참조)를 추가 합니다.

tooadd 사용자, 세션, 이벤트 또는 보존 섹션 tooyour 통합 문서를 사용 하 여 hello **사용자 추가** 또는 기타 해당 단추 hello hello 통합 문서 맨 아래에 또는 hello 섹션 맨 아래에 있습니다.

![통합 문서의 사용자 섹션](./media/app-insights-usage-workbooks/users-section.png)

**사용자** 섹션은 "내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 사용자의 수는?"에 응답합니다.

**세션** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용하는 데 소비한 세션의 수는?"에 응답합니다.

**이벤트** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 시간은?"에 응답합니다.

이러한 각 유형의 세 가지 섹션을 hello 컨트롤 및 시각화의 동일한 집합 제공합니다.

* [사용자, 세션 및 이벤트 섹션 편집에 대한 자세한 정보](app-insights-usage-segmentation.md)
* Hello 기본 차트, 히스토그램 표, 자동 insights 및 hello를 사용 하 여 샘플 사용자 시각화를 설정/해제 **차트 표시**, **눈금 표시**, **표시 Insights**, 및 **이러한 사용자가 샘플** hello 위쪽 각 섹션의 확인란을 선택 합니다.

![통합 문서의 재방문 주기 섹션](./media/app-insights-usage-workbooks/retention-section.png)

**재방문 주기** 섹션은 "1일 또는 1주일에 일부 페이지를 보거나 일부 기능을 사용한 사용자 중 다음 날이나 다음 주에 다시 방문한 사용자 수는?"에 응답합니다.

* [재방문 주기 섹션 편집에 대한 자세한 정보](app-insights-usage-retention.md)
* 설정/해제 hello 선택적인 전반적인 보존 차트 hello를 사용 하 여 **표시 전반적인 보존 차트** hello 위쪽 hello 섹션의 확인란을 선택 합니다.

## <a name="adding-application-insights-analytics-sections"></a>Application Insights 분석 섹션 추가

![통합 문서의 분석 섹션](./media/app-insights-usage-workbooks/analytics-section.png)

응용 프로그램 통찰력 분석 쿼리 섹션 tooyour 통합 tooadd hello를 사용 하 여 **추가 분석 쿼리에서** hello hello 통합 문서 맨 아래에 또는 만큼의 hello 아래쪽 단추입니다.

분석 쿼리 섹션을 사용하면 통합 문서에 Application Insights 데이터에 대해 임의 쿼리를 추가할 수 있습니다. 이러한 유연성 분석 쿼리 섹션 프로그램 go toofor hello와 같은 사용자, 세션, 이벤트 및 보존에 대 한 위에 나열 된 4 아닌 다른 사이트에 대 한 모든 질문에 대답 해야 합니다.을 의미 합니다.

* 예외 수 않은 사용량에서 감소 기간 시간이 hello 하는 동안 사용자 사이트 throw?
* 일부 페이지를 보는 사용자에 대 한 페이지 로드 시간의 hello 분포는 무엇 이었습니까?
* 사이트의 일부 페이지 집합을 봤지만 다른 일부 페이지 집합을 보지 않은 사용자의 수는? 다른 사이트의 기능 하위 집합을 사용 하는 사용자의 클러스터가 있는 경우 유용 toounderstand 수 있습니다 (hello를 사용 하 여 `join` hello로 연산자 `kind=leftanti` hello 로그 분석 쿼리 언어에서에서 한정자).

사용 하 여 hello [로그 분석 쿼리 언어 참조](https://docs.loganalytics.io/) toolearn 쿼리를 작성 하는 방법에 대 한 자세한 합니다.

## <a name="adding-text-and-markdown-sections"></a>텍스트 및 Markdown 섹션 추가

제목, 설명 및 해설 tooyour 통합 문서 추가 narrative 테이블 및 차트의 집합을 변환 하는 데 도움이 됩니다. 통합 문서에 텍스트 부분 지원 hello [마크 다운 구문](https://daringfireball.net/projects/markdown/) 텍스트 서식 지정, 머리글, 굵게, 기울임꼴 등 글머리 기호 목록에 대 한 합니다.

tooadd 텍스트 섹션 tooyour 통합 문서를 사용 하 여 hello **텍스트 추가** 단추 hello hello 통합 문서 맨 아래에 또는 hello 섹션 맨 아래에 있습니다.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>팀과 통합 문서 저장 및 공유

Hello에는 Application Insights 리소스 내에서 통합 문서 저장 **내 보고서** 개인 tooyou 인 구역 또는 hello **공유 보고서** 섹션에 액세스할 수 있는 액세스 가능한 tooeveryone Application Insights 리소스 toohello 합니다. tooview hello 리소스에서 모든 hello 통합 문서 클릭 hello **열려** hello 작업 모음에서 단추입니다.

통합 문서에 현재 있는 tooshare **내 보고서**:

1. 클릭 **열려** hello 작업 모음에
2. Hello "..." 단추를 클릭 hello 통합 문서 옆에 있는 tooshare
3. 클릭 **tooShared 보고서 이동**합니다.

통합 문서 링크와 함께 또는 전자 메일을 통해 tooshare 클릭 **공유** hello 작업 모음에서 합니다. Hello 링크의 받는 사람에 게 hello Azure 포털 tooview hello 통합 문서에서 toothis 리소스에 액세스할 필요 있음을 염두에서에 둬야 합니다. toomake 편집 받는 사람에 게 필요 이상의 참가자 권한을 hello 리소스에 대 한 합니다.

Azure 대시보드 링크 tooa 통합 문서 tooan toopin:

1. 클릭 **열려** hello 작업 모음에
2. Hello "..." 단추를 클릭 hello 통합 문서 옆에 있는 toopin
3. 클릭 **Pin toodashboard**합니다.

## <a name="next-steps"></a>다음 단계

## <a name="next-steps"></a>다음 단계
- tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.
- 사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.
    - [사용자, 세션, 이벤트](app-insights-usage-segmentation.md)
    - [깔때기](usage-funnels.md)
    - [보존](app-insights-usage-retention.md)
    - [사용자 흐름](app-insights-usage-flows.md)
    - [사용자 컨텍스트 추가](app-insights-usage-send-user-context.md)
    

---
title: "aaaExport 로그 분석 데이터 tooPower BI | Microsoft Docs"
description: "Power BI는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.  로그 분석 지속적으로 내보낼 수 데이터 hello OMS 저장소에서 Power BI로 하므로 해당 시각화 및 분석 도구를 활용할 수 있습니다.  이 문서에서는 일정 한 간격으로 자동으로 BI tooPower를 내보내는 로그 분석의 tooconfigure 쿼리 하는 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>로그 분석 데이터 tooPower BI 내보내기

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 로그 분석 데이터 tooPower BI 내보내기에 대 한이 과정은 더 이상 작동 합니다.  그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다. 
>
> 업그레이드 후 Azure 로그 분석 사용 하 여 hello Application Insights와 같은 플랫폼 및 동일한 프로세스으로 tooexport 로그 분석 쿼리 tooPower BI hello를 사용 하 여 [hello 프로세스 tooexport Application Insights 쿼리 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)합니다.  해당 문서에 설명 된 대로 hello 분석 콘솔을 사용 하 여 hello 쿼리를 내보낸 하거나 hello를 선택할 수 있습니다 **Power BI** hello hello 로그 검색 포털의 hello 화면 위쪽에 단추입니다.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)는 서로 다른 데이터 집합의 분석을 위해 다양한 시각화 및 보고서를 제공하는 Microsoft의 클라우드 기반 비즈니스 분석 서비스입니다.  로그 분석 자동으로 내보낼 수 데이터 hello OMS 저장소에서 Power BI로 하므로 해당 시각화 및 분석 도구를 활용할 수 있습니다.

로그 분석을 Power BI를 구성할 때 Power BI에서 데이터 집합 결과 toocorresponding 내보내기 로그 쿼리를 만듭니다.  hello 쿼리 및 내보내기 tooautomatically 로그 분석에 의해 수집 된 hello 최신 데이터와 toodate tookeep hello 데이터 집합을 정의 하는 일정에 따라 실행을 계속 합니다.

![로그 분석 tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Power BI 일정
A *Power BI 일정* hello OMS 리포지토리에 tooa 해당 데이터 집합에서 Power BI 및이 검색은 tookeep hello 데이터 집합 현재을 실행 하는 빈도 정의 하는 일정에서 데이터 집합을 내보내는 로그 검색에 포함 됩니다.

hello 데이터 집합의 hello 필드 hello 로그 검색에서 반환 된 hello 레코드의 hello 속성 일치 합니다.  Hello 검색 hello 데이터 집합의 모두 포함 되며 다음 다양 한 종류의 레코드를 반환 하는 경우 각각 hello의 hello 속성이 레코드 종류를 포함 합니다.  

> [!NOTE]
> 모범 사례 toouse와 같은 명령을 사용 하 여 모든 통합 것과 반대로 tooperforming으로 원시 데이터를 반환 하는 로그 검색 쿼리는 [측정값](log-analytics-search-reference.md#measure)합니다.  Hello 원시 데이터에서 Power BI에서 모든 집계 및 계산을 수행할 수 있습니다.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>OMS 작업 영역 tooPower BI를 연결합니다.
로그 분석 tooPower BI에서에서 내보낼 수 있습니다, 전에 절차를 수행 하는 hello를 사용 하 여 OMS 작업 영역 tooyour Power BI 계정을 연결 해야 합니다.  

1. Hello OMS 콘솔에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. **계정**을 선택합니다.
3. Hello에 **작업 영역 정보** 섹션 클릭 **tooPower BI 계정 연결**합니다.
4. Power BI 계정에 대 한 hello 자격 증명을 입력 합니다.

## <a name="create-a-power-bi-schedule"></a>Power BI 일정 만들기
절차를 수행 하는 hello를 사용 하 여 각 데이터 집합에 대 한 Power BI 일정을 만듭니다.

1. Hello OMS 콘솔에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.
2. 새 쿼리를 입력 하거나 선택 hello tooexport 너무 되도록 데이터를 반환 하는 저장된 된 검색**Power BI**합니다.  
3. Hello 클릭 **Power BI** hello 페이지 tooopen hello hello 위쪽에 단추 **Power BI** 대화 상자.
4. 다음 테이블을 클릭 하 여 hello에 hello 정보를 제공 **저장**합니다.

| 속성 | 설명 |
|:--- |:--- |
| 이름 |이름 tooidentify hello 일정의 Power BI 일정 hello 목록을 볼 때입니다. |
| 저장된 검색 |로그 검색 toorun hello 합니다.  Hello 현재 쿼리를 선택 하거나 hello 드롭다운 상자에서 기존 저장 된 검색을 선택 합니다. |
| 일정 |얼마나 자주 저장 toorun hello 검색 및 toohello Power BI 데이터 집합을 내보내기.  hello 값은 15 분에서 24 시간 사이 여야 합니다. |
| 데이터 집합 이름 |Power BI의 hello 데이터 집합의 hello 이름입니다.  존재하지 않는 경우 생성되고 존재하는 경우 업데이트됩니다. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Power BI 일정 보기 및 제거
절차를 수행 하는 hello 사용 하 여 기존 Power BI 일정의 보기 hello 목록입니다.

1. Hello OMS 콘솔에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. **Power BI**를 선택합니다.

또한 hello의 toohello 세부 정보를 예약 하 고 hello 횟수를 일정 hello 지난 주 hello에서 실행 된 hello hello 마지막 동기화 상태를 표시 됩니다.  Hello 동기화 오류가 발생 하면 hello 링크 toorun hello 오류의 세부 정보를 레코드에 대 한 로그 검색 클릭 수 있습니다.

Hello를 클릭 하 여 일정을 제거할 수 있습니다 **X** hello에 **제거 열**합니다.  **끄기**를 선택하여 일정을 비활성화할 수 있습니다.  toomodify 일정을 제거 하며 hello 새 설정으로 다시 만듭니다.

![Power BI 일정](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>샘플 연습
hello 다음 섹션 안내 Power BI 작업을 예약 하 고 해당 데이터 집합 toocreate를 사용 하 여의 예는 간단한 보고서.  이 예제에서는 일련의 컴퓨터에 대 한 모든 성능 데이터 내보낸된 tooPower BI 이며 선 그래프 toodisplay 프로세서 사용률을 작성 합니다.

### <a name="create-log-search"></a>로그 검색 만들기
Toosend toohello dataset 한다고 hello 데이터에 대 한 로그 검색을 만들어 시작 합니다.  이 예제에서는 *srv*로 시작하는 이름의 컴퓨터에 대한 모든 성능 데이터를 반환하는 쿼리를 사용합니다.  

![Power BI 일정](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Power BI 검색 만들기
Hello 클릭 **Power BI** tooopen hello Power BI 대화 상자 단추 및 hello 필요한 정보를 제공 합니다.  이 검색 toorun 시간 마다 한 번씩 원하는 하 고 라는 데이터 집합을 만들 *Contoso 성능*합니다.  Hello 기본값인 방지 개이므로 이미 hello 데이터를 원하는 만듭니다 hello 검색 열기, *현재 검색 쿼리 사용* 에 대 한 **저장 된 검색**합니다.

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Power BI 검색 확인
tooverify hello 일정을 올바르게 만든 म, म hello에서 Power BI 검색 hello 목록을 볼 **설정** hello OMS 대시보드에 타일입니다.  몇 분 정도 기다린 하 고 보고 hello 동기화가 실행 될 때까지이 보기를 새로 고칩니다.

![Power BI 검색](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Power BI에서 데이터 집합 hello를 확인 합니다.
이 계정에 로그인 했습니다 [powerbi.microsoft.com](http://powerbi.microsoft.com/) 너무 스크롤하여**데이터 집합** hello hello 왼쪽된 창의 맨 아래에 있습니다.  해당 hello 볼 수 있습니다 *Contoso 성능* 우리의 내보내기 성공적으로 실행 되었음을 나타내는 데이터 집합 나열 됩니다.

![Power BI 데이터 집합](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>데이터 집합 기반 보고서 만들기
Hello 선택 **Contoso 성능** 데이터 집합을 클릭 하 고 **결과** hello에 **필드** 이 데이터 집합의 일부인 hello 오른쪽 tooview hello 필드에는 창입니다.  각 컴퓨터에 대 한 선 그래프 보여 주는 프로세서 사용률 toocreate hello 다음 작업을 수행 합니다.

1. Hello 꺾은선형 차트 시각화를 선택 합니다.
2. 끌기 **ObjectName** 너무**보고서 수준 필터** 확인 **프로세서**합니다.
3. 끌기 **: _total CounterName** 너무**보고서 수준 필터** 확인 **% Processor Time**합니다.
4. 끌기 **CounterValue** 너무**값**합니다.
5. 끌기 **컴퓨터** 너무**범례**합니다.
6. 끌기 **TimeGenerated** 너무**축**합니다.

이 데이터 집합의 hello 데이터로 해당 hello 결과 선 그래프를 표시 하는 것을 볼 수 있습니다.

![Power BI 꺾은선형 그래프](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Hello 보고서 저장
Hello를 클릭 하 여 hello 보고서 저장 우리 hello hello 화면 위쪽에 단추를 저장 하 고 hello 왼쪽된 창에서 hello 보고서 섹션에 나열 된 이제 유효성 검사.

![Power BI 보고서](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) toobuild 쿼리 될 수 있는 내보낸 tooPower BI 합니다.
* 에 대 한 자세한 내용은 [Power BI](http://powerbi.microsoft.com) 내보내기 로그 분석에 따라 toobuild 시각화 합니다.

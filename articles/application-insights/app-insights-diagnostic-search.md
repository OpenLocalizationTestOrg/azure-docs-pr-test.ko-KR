---
title: "Azure Application Insights에서 검색 aaaUsing | Microsoft Docs"
description: "웹앱에서 전송된 원시 원격 분석을 검색하고 필터링합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Application Insights에서 Search 사용
검색의 기능은 [Application Insights](app-insights-overview.md) 하거나 사용할 수 있는 toofind 및 페이지 보기, 예외 등의 개별 원격 분석 항목을 탐색 웹 요청 합니다. 또한 코딩한 로그 추적 및 이벤트를 볼 수 있습니다.

(사용자 데이터에 비해 좀 더 복잡한 쿼리를 위해서는 [Analytics](app-insights-analytics-tour.md)를 사용합니다.)

## <a name="where-do-you-see-search"></a>Search 기능은 어디에 있나요?
### <a name="in-hello-azure-portal"></a>Hello Azure 포털에서
응용 프로그램의 응용 프로그램 Insights 개요 블레이드에 hello에서 진단 검색을 명시적으로 열 수 있습니다.

![진단 검색 열기](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

일부 차트와 표 항목을 클릭할 때에도 열립니다. 이 경우 해당 필터 선택한 항목의 hello 형식에 toofocus를 설정 미리 됩니다. 

예를 들어 hello 개요 블레이드에 없습니다는 요청 응답 시간에 따라 분류 가로 막대형 차트입니다. 클릭 하 여 성능 범위 toosee 개별 요청의 목록을 응답 시간 범위에:

![요청 성능 클릭](./media/app-insights-diagnostic-search/07-open-from-filters.png)

hello 진단 검색의 본문은 목록 뷰, 사용자가 코딩 하는 사용자 지정 이벤트 및 등 페이지 원격 분석 항목-서버 요청 합니다. Hello hello 목록의 맨은 시간이 지남에 따라 이벤트 수를 표시 하는 요약 차트입니다.

새로 고침 tooget 새 이벤트를 클릭 합니다.

### <a name="in-visual-studio"></a>Visual Studio에서

Visual Studio에는 Application Insights 검색 창도 있습니다. 디버그 중인 hello 응용 프로그램에 의해 생성 되는 원격 분석 이벤트를 표시 하기 위한 가장 유용 합니다. 하지만 hello Azure 포털에서 게시 된 앱에서 수집 된 hello 이벤트를 표시할 수도 있습니다.

Visual Studio에서 hello 검색 창을 엽니다.

![Visual Studio에서 열린 Application Insights 검색](./media/app-insights-diagnostic-search/32.png)

hello 검색 창 기능이 비슷한 toohello 웹 포털을 있습니다.

![Visual Studio Application Insights 검색 창](./media/app-insights-diagnostic-search/34.png)

요청 또는 페이지 보기를 연 hello 추적 작업 탭을 사용할 수 있습니다. ' 작업이 ' tooa 단일 요청 또는 페이지 보기와 연결 된 이벤트의 시퀀스입니다. 예를 들어 종속성 호출, 예외, 추적 로그 및 사용자 지정 이벤트는 단일 연산의 일부일 수 있습니다. hello 추적 작업 탭에서는 타이밍 및 관계 toohello 요청 또는 페이지 보기의 이러한 이벤트의 기간에 그래픽으로 hello 합니다. 

## <a name="inspect-individual-items"></a>개별 항목 검사
모든 원격 분석 항목 toosee 키 필드 및 관련된 항목을 선택 합니다. Toosee hello 전체 필드 집합 "..."를 클릭 합니다. 

![새 작업 항목을 클릭 하 고 hello 필드를 편집한 다음 확인을 클릭 합니다.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>이벤트 유형 필터링
Hello 필터 블레이드를 열고 hello 이벤트 형식 선택 toosee 원하는 합니다. (Toorestore hello 필터 hello 블레이드를 연 원하는 나중 하는 경우 재설정 클릭 합니다.)

![필터 선택 및 원격 분석 유형 선택](./media/app-insights-diagnostic-search/02-filter-req.png)

hello 이벤트 유형은 다음과 같습니다.

* **추적** -  TrackTrace, log4Net, NLog 및 System.Diagnostic.Trace 호출을 포함한 [진단 로그](app-insights-asp-net-trace-logs.md)입니다.
* **요청** - 페이지, 스크립트, 이미지, 스타일 파일 및 데이터를 포함하는 서버 응용 프로그램이 수신하는 HTTP 요청입니다. 이러한 이벤트는 사용 되는 toocreate hello 요청 및 응답 개요 차트입니다.
* **페이지 보기** - [hello 웹 클라이언트에서 보낸 원격 분석](app-insights-javascript.md), toocreate 페이지, 보고서 보기를 사용 합니다. 
* **사용자 지정 이벤트** -너무 순서 대로 호출 tooTrackEvent()을 삽입 하는 경우[사용을 모니터링](app-insights-api-custom-events-metrics.md), 여기서 검색할 수 있습니다.
* **예외** -확인할 수 없는 [hello 서버에서 예외](app-insights-asp-net-exceptions.md), trackexception ()를 사용 하 여 로그인 하 고 있습니다.
* **종속성** - [서버 응용 프로그램에서 호출](app-insights-asp-net-dependencies.md) tooother 데이터베이스 또는 REST Api와 같은 서비스를 제공 하며에서 AJAX 호출 프로그램 [클라이언트 코드](app-insights-javascript.md)합니다.
* **가용성** - [가용성 테스트](app-insights-monitor-web-app-availability.md)의 결과입니다.

## <a name="filter-on-property-values"></a>속성 값에서 필터링
Hello 속성 값에 대 한 이벤트를 필터링 할 수 있습니다. hello 사용 가능한 속성 선택한 hello 이벤트 유형에 따라 달라 집니다. 

예를들어 특정 응답 코드에 대한 요청을 선택합니다. 

![속성 확장 및 값 선택](./media/app-insights-diagnostic-search/03-response500.png)

특정 속성의 값이 없는 선택 하면 모든 값을 선택 효과가 같음 hello가 있습니다. 해당 속성에서 필터링을 전한합니다.

### <a name="narrow-your-search"></a>검색 범위 좁히기
해당 hello toohello hello 필터 값의 오른쪽을 계산 하는 알림 횟수 있습니다 hello 현재 필터링 된 집합에는 표시 합니다. 

이 예제에서는 '500' hello 오류는 대부분 해당 hello ' Rpt/직원 ' 요청으로 인해 지우기입니다.

![속성 확장 및 값 선택](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Hello로 이벤트를 찾을 동일한 속성
동일한 hello로 모든 hello 찾기 항목 속성 값:

![마우스 오른쪽 단추로 속성 클릭](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Hello 데이터 검색

> [!NOTE]
> toowrite 더 복잡 한 쿼리 열기 [ **분석** ](app-insights-analytics-tour.md) hello hello 검색 블레이드 맨 위에서 합니다.
> 

단어 hello 속성 값 중 하나에 대해 검색할 수 있습니다. 속성 값을 포함하는 [사용자 지정 이벤트](app-insights-api-custom-events-metrics.md)를 작성한 경우에 특히 유용합니다. 

시간 범위를 더 짧은 범위 검색으로는 더 빠르게 tooset을 할 수 있습니다. 

![진단 검색 열기](./media/app-insights-diagnostic-search/appinsights-311search.png)

하위 문자열이 아닌 전체 단어를 검색합니다. 인용 부호 tooenclose 특수 문자를 사용 합니다.

| string | 해당 문자열을 검색하지 *않는* 용어 | 해당 용어가 검색되는 문자열 |
| --- | --- | --- |
| HomeController.About |home<br/>controller<br/>out | homecontroller<br/>about<br/>"homecontroller.about"|
|미국|Uni<br/>ted|united<br/>states<br/>united AND states<br/>"united states"

다음은 사용할 수 있습니다 hello 검색 식입니다.

| 샘플 쿼리 | 결과 |
| --- | --- |
| `apple` |해당 필드가 hello 단어가 "apple"를 포함 하는 hello 시간 범위에서 모든 이벤트를 찾습니다. |
| `apple AND banana` |두 단어를 모두 포함하는 이벤트를 찾습니다. "and"가 아닌 대문자 "AND"를 사용하세요. |
| `apple OR banana`<br/>`apple banana` |둘 중 한 단어를 포함하는 이벤트를 찾습니다. "or"가 아닌 "OR"을 사용하세요.<br/>약식입니다. |
| `apple NOT banana` |한 단어를 포함 하지 hello 다른 이벤트를 찾습니다. |



## <a name="sampling"></a>샘플링
앱 원격 분석을 많이 생성 하는 경우 (ASP.NET SDK 버전 2.0.0-beta3 hello를 사용 하는 및 이상 버전), hello 적응 샘플링 모듈 toohello 포털 이벤트의 대표 일부만 전송 하 여 전송 된 hello 볼륨을 자동으로 줄입니다. 그러나 이벤트 하는 동일한 요청 선택 되거나 그룹으로 선택이 취소 관련된 toohello 관련된 이벤트를 탐색할 수 있도록 합니다. 

[샘플링에 대해 알아봅니다](app-insights-sampling.md).



## <a name="create-work-item"></a>작업 항목 만들기
GitHub 또는 Visual Studio Team Services에서 모든 원격 분석 항목의 hello 정보로 버그를 만들 수 있습니다. 

![새 작업 항목을 클릭 하 고 hello 필드를 편집한 다음 확인을 클릭 합니다.](./media/app-insights-diagnostic-search/42.png)

hello 처음으로 작업을 수행 하 라는 메시지가 표시 됩니다 tooconfigure 링크 tooyour Team Services 계정 및 프로젝트 합니다.

![Team Services 서버 및 hello 프로젝트 이름을의 hello URL을 입력 하 고 권한 부여를 클릭](./media/app-insights-diagnostic-search/41.png)

(또한에서 구성할 수 있습니다 hello 링크를 hello 작업 항목 블레이드.)

## <a name="save-your-search"></a>검색 저장
원하는 모든 hello 필터를 설정한 경우 hello 검색을 즐겨찾기에 저장할 수 있습니다. 조직 계정에서 작업 하는 경우 선택할 수 있습니다 여부 tooshare 다른 팀 멤버와 해당 합니다.

![즐겨찾기 클릭 hello 이름을 설정 하 고 저장을 클릭합니다](./media/app-insights-diagnostic-search/08-favorite-save.png)

toosee hello 다시 검색 **이동 toohello 개요 블레이드에** 즐겨찾기를 엽니다.

![즐겨찾기 타일](./media/app-insights-diagnostic-search/09-favorite-get.png)

상대 시간 범위와 함께 저장 하는 경우 다시 열된 블레이드 hello에 hello 최신 데이터가 있습니다. Hello 절대 시간 범위와 함께 저장 하는 경우 표시 될 때마다 동일한 데이터입니다. ('Relative'를 사용할 수 없으면 toosave를 즐겨찾기에 추가 하려는 경우 hello 헤더의 시간 범위를 클릭 및 사용자 지정 범위를 시간 범위를 설정 합니다.)

## <a name="send-more-telemetry-tooapplication-insights"></a>TooApplication Insights 더 많은 원격 분석 보내기
또한 toohello 기본적으로 원격 분석에서 Application Insights SDK에서 보낸, 다음을 수행할 수 있습니다.

* [.NET](app-insights-asp-net-trace-logs.md) 또는 [Java](app-insights-java-trace-logs.md)의 즐겨찾는 로깅 프레임워크에서 로그 추적을 캡처합니다. 이는 로그 추적을 통해 검색하고 페이지 보기, 예외 사항 및 기타 이벤트와 상관 관계를 지정할 수 있음을 의미합니다. 
* [코드를 작성](app-insights-api-custom-events-metrics.md) toosend 사용자 지정 이벤트, 페이지 보기 및 예외입니다. 

[Toosend 기록 하는 방법 및 사용자 지정 원격 분석 tooApplication Insights에 알아봅니다](app-insights-asp-net-trace-logs.md)합니다.

## <a name="questions"></a>질문 및 답변
### <a name="limits"></a>얼마나 많은 데이터가 보존되나요?

Hello 참조 [제한 요약](app-insights-pricing.md#limits-summary)합니다.

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>내 서버 요청에서 게시 데이터를 어떻게 볼 수 있나요?
म hello 게시 데이터를 자동으로 기록 하지 않지만 사용할 수 있습니다 [TrackTrace 또는 로그 호출](app-insights-asp-net-trace-logs.md)합니다. Hello 메시지 매개 변수에서 hello 게시 데이터를 배치 합니다. 필터링 할 수 없습니다 hello 메시지 hello에 동일한 hello 크기 제한을 더 긴 하지만 방식으로 속성을 필터링 할 수 있습니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>다음 단계
* [분석에서 복잡한 쿼리 작성](app-insights-analytics-tour.md)
* [TooApplication Insights 로그 및 사용자 지정 원격 분석 보내기](app-insights-asp-net-trace-logs.md)
* [가용성 및 응답성 테스트 설정](app-insights-monitor-web-app-availability.md)
* [문제 해결](app-insights-troubleshoot-faq.md)

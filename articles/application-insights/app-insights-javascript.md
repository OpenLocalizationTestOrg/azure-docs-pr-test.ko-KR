---
title: "JavaScript 용 aaaAzure Application Insights 웹 앱 | Microsoft Docs"
description: "페이지 보기 및 세션 수와 웹 클라이언트 데이터를 가져오고 사용 패턴을 추적합니다. JavaScript 웹 페이지의 예외 및 성능 문제를 감지합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>웹 페이지용 Application Insights
Hello 성능 및 웹 페이지 또는 응용 프로그램의 사용에 대해 알아봅니다. 추가 하는 경우 [Application Insights](app-insights-overview.md) 타이밍의 페이지 로드 및 AJAX 호출, 개수 및 브라우저 예외 AJAX 오류 뿐만 아니라 사용자 및 세션 수의 세부 정보를 가져올 tooyour 페이지 스크립트입니다. 이러한 모든 요소를 페이지, 클라이언트 OS 및 브라우저 버전, 지리적 위치 및 기타 차원으로 분할할 수 있습니다. 실패 횟수 또는 느린 페이지 로딩에 대한 경고를 설정할 수도 있습니다. 및 JavaScript 코드에 추적 호출을 삽입 하 여 추적할 수 있습니다 hello 웹 페이지 응용 프로그램의 다른 기능을 사용 방법입니다.

Application Insights는 다른 웹 페이지와 함께 사용할 수 있습니다. 간단한 JavaScript만 추가하면 됩니다. 웹 서비스가 [Java](app-insights-java-get-started.md) 또한 [ASP.NET](app-insights-asp-net.md)인 경우, 서버 및 클라이언트의 원격 분석을 통합할 수 있습니다.

![portal.azure.com에서 앱의 리소스 열고 브라우저를 클릭합니다.](./media/app-insights-javascript/03.png)

구독이 너무 필요[Microsoft Azure](https://azure.com)합니다. 팀이 조직 구독을 하는 경우 Microsoft 계정 tooit hello 소유자 tooadd 요청. 개발 및 소규모 사용에는 별도의 비용이 없습니다.

## <a name="set-up-application-insights-for-your-web-page"></a>웹 페이지용 Application Insights 설치
다음과 같이 hello 로더 코드 조각 tooyour 웹 페이지를 추가 합니다.

### <a name="open-or-create-application-insights-resource"></a>Application Insights 리소스 열기 또는 만들기
Application Insights 리소스 hello 페이지의 성능 및 사용에 대 한 데이터가 표시 되는 위치입니다. 

[Azure Portal](https://portal.azure.com)에 로그인합니다.

이미 앱의 서버 쪽 hello에 대 한 모니터링을 설정 하면 리소스를 이미 합니다.

![찾아보기, 개발자 서비스, Application Insights를 선택합니다.](./media/app-insights-javascript/01-find.png)

계정이 없는 경우 계정을 만듭니다.

![새로 만들기, 개발자 서비스, Application Insights를 선택합니다.](./media/app-insights-javascript/01-create.png)

*벌써 질문이 있나요?* [리소스 만들기에 대해 자세히 알아보세요](app-insights-create-new-resource.md)를 구독해야 합니다.

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Hello SDK 스크립트 tooyour 앱 또는 웹 페이지 추가
빠른 시작에서 웹 페이지에 대 한 hello 스크립트를 얻습니다.

![응용 프로그램 개요 블레이드를 사용 하 여 빠른 시작을 선택에서 내 웹 페이지 코드 toomonitor 가져오기 합니다. Hello 스크립트를 복사 합니다.](./media/app-insights-javascript/02-monitor-web-page.png)

Hello 하기 바로 전에 hello 스크립트 삽입 `</head>` 태그 tootrack 모든 페이지의 원하는 합니다. 웹 사이트에서 마스터 페이지, 경우에 hello 스크립트 있습니다 넣을 수 있습니다. 예:

* ASP.NET MVC 프로젝트에서는 `View\Shared\_Layout.cshtml`
* Hello 제어판에 있는 SharePoint 사이트에서 엽니다 [사이트 설정 / 마스터 페이지](app-insights-sharepoint.md)합니다.

hello 스크립트 hello 데이터 tooyour Application Insights 리소스를 알려 주는 hello 계측 키를 포함 합니다. 

([Hello 스크립트의입니다. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(잘 알려진 웹 페이지 프레임워크를 사용하는 경우 Application Insights 어댑터를 찾아보세요. 예를 들어 [AngularJS 모듈](http://ngmodules.org/modules/angular-appinsights)이 있습니다.)*

## <a name="detailed-configuration"></a>자세한 구성
몇 가지 [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)를 설정할 수 있지만 대부분의 경우에서 설정할 필요가 없습니다. 예를 들어 사용 하지 않도록 설정 하거나 hello 페이지 보기 (tooreduce 트래픽) 당 보고 Ajax 호출 수가 제한 수 있습니다. 또는 일괄 처리 되 고 없이 디버그 모드 toohave 원격 분석 이동 hello 파이프라인을 통해 신속 하 게 설정할 수 있습니다.

tooset 이러한 매개 변수 hello 코드 조각에서이 줄 찾아 그 뒤 쉼표로 구분 된 항목을 더 추가 합니다.

    })({
      instrumentationKey: "..."
      // Insert here
    });

hello [사용 가능한 매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) 포함:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>앱 실행
웹 응용 프로그램 실행, 한 toogenerate 원격 분석 및 a 몇 초 정도 대기 하는 동안 합니다. Hello를 사용 하 여 하거나 실행할 수 있습니다 **F5** 하려면 개발 컴퓨터에 키 또는 게시 하 고 사용자가를 사용할 수 있도록 합니다.

브라우저의 디버깅 도구를 사용 하 여 tooApplication Insights 웹 앱을 보내는 지 toocheck hello 원격 분석 하려는 경우 (**F12** 다양 한 브라우저에). 데이터 toodc.services.visualstudio.com을 전송 됩니다.

## <a name="explore-your-browser-performance-data"></a>브라우저 성능 데이터 탐색
사용자의 브라우저에서 성능 데이터를 집계 하는 브라우저 블레이드 tooshow hello를 엽니다.

![Portal.azure.com에서 앱의 리소스 열고 설정, 브라우저를 클릭합니다.](./media/app-insights-javascript/03.png)

*아직 아무 데이터도 없나요? 클릭 **새로 고침** hello hello 페이지 위쪽에 있습니다. 여전히 아무 데이터도 없나요? [문제 해결](app-insights-troubleshoot-faq.md)을 참조하세요.*

hello 브라우저 블레이드는는 [메트릭 탐색기 블레이드의](app-insights-metrics-explorer.md) 미리 설정 된 필터 및 차트 선택을 사용 합니다. Hello 시간 범위, 필터 및 차트 구성 및 즐겨찾기에 hello 결과 저장 하는 경우 편집할 수 있습니다. 클릭 **기본값 복원** tooget 백 toohello 원래 블레이드 구성 합니다.

## <a name="page-load-performance"></a>페이지 로드 성능
Hello에 top은 페이지 로드 시간을 세그먼트 차트입니다. hello hello 차트의 전체 높이 사용자의 브라우저에서 응용 프로그램에서 hello 평균 시간 tooload 및 표시 페이지를 나타냅니다. hello 브라우저 이벤트가 처리, 레이아웃 및 실행 중인 스크립트를 포함 하 여 모든 동기 로드 될 때까지 hello 초기 HTTP 요청을 보낼 때 hello 시간에서 측정 됩니다. AJAX 호출로부터 웹 파트를 로드하는 등의 비동기 작업은 포함되지 않습니다.

hello로 hello 총 페이지 로드 시간을 분할 하는 hello 차트 [W3C에서 정의 된 표준 타이밍이](http://www.w3.org/TR/navigation-timing/#processing-model)합니다. 

![](./media/app-insights-javascript/08-client-split.png)

해당 hello 참고 *네트워크 연결* hello 브라우저 toohello 서버에서의 모든 요청을 통해 평균 이기 때문에 시간은 예상 보다 낮은 경우가 많습니다. 활성 연결 toohello 서버 이미 있기 때문에 0의 연결 시간을 포함 하는 많은 개별 요청.

### <a name="slow-loading"></a>로드가 느립니까?
느린 페이지 로드는 사용자가 가장 불만족을 느끼는 부분입니다. Hello 차트 느린 페이지 로드를 나타내는 경우 쉽게 toodo 몇 가지 진단 조사 합니다.

hello 차트 응용 프로그램에서 모든 페이지를 로드할의 hello 평균을 보여 줍니다. hello 문제가 발생 한 경우 toosee 제한 tooparticular 페이지, hello 블레이드 아래쪽 모양을 추가, 기준으로 분할 하는 표는이 페이지 URL:

![](./media/app-insights-javascript/09-page-perf.png)

Hello 페이지 보기 수 및 표준 편차를 확인 합니다. Hello 페이지 수를 매우 낮은 경우 다음 hello 문제 되지에 영향을 주는 사용자 훨씬 합니다. 높은 표준 편차 (자체가 비교 가능한 toohello 평균)의 개별 측정값 간의 편차 많은 나타냅니다.

**한 URL 및 한 페이지 보기에서 확대합니다.** 모든 페이지 이름 toosee 브라우저 차트 필터링 된 정당한 toothat URL; 블레이드를 클릭 합니다. 및 다음에서 페이지 보기의 인스턴스.

![](./media/app-insights-javascript/35.png)

클릭 `...` 해당 이벤트에 대 한 속성의 전체 목록은 또는 hello Ajax 호출 및 관련된 이벤트를 검사 합니다. 느린 Ajax 호출 hello에 영향을 전체 페이지 로드 시간 동기 경우. Hello에 대 한 서버 요청을 포함 하는 이벤트와 관련 된 동일한 URL (설정한 경우 Application Insights를 웹 서버에서).

**시간에 따른 페이지 성능** Hello 브라우저 블레이드를 다시 최대치 특정 시간에 없는 경우 hello 페이지 보기 로드 시간 그리드 꺾은선형 차트 toosee로 변경 합니다.

![Hello 눈금의 hello 헤드를 클릭 하 고 새 차트 종류를 선택 합니다.](./media/app-insights-javascript/10-page-perf-area.png)

**다른 차원으로 분류** 어쩌면 페이지 느린 tooload 특정 브라우저, 운영 체제, 클라이언트 또는 사용자 위치에 있는? 새 차트를 추가 하 고 hello 시험해 **Group by** 차원입니다.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>AJAX 성능
웹 페이지의 모든 AJAX 호출이 정상적으로 수행되고 있는지 확인합니다. 페이지의 사용 되는 toofill 부분 비동기적으로 되어 있습니다. Hello 전체 페이지 수 로드 신속 하 게 하지만 사용자가 수 수 실망 빈 웹 파트에서 시작 하 여 그 안의 데이터 tooappear 대기 합니다.

웹 페이지에서 AJAX 호출 hello 브라우저 블레이드를 종속성으로 표시 됩니다.

요약 차트 hello hello 블레이드 위쪽 부분에 있습니다.

![](./media/app-insights-javascript/31.png)

그리고 상세한 표가 아래에 있습니다.

![](./media/app-insights-javascript/33.png)

특정 세부 정보를 보려면 행을 클릭합니다.

> [!NOTE]
> Hello 블레이드에서 hello 브라우저 필터를 삭제 하면 서버와 AJAX 종속성 이러한 차트에 포함 됩니다. 기본값 복원 tooreconfigure hello 필터를 클릭 합니다.
> 
> 

**실패 한 Ajax 호출으로 toodrill** toohello 종속성 오류 눈금선 아래로 스크롤한 다음 행 toosee 특정 인스턴스를 클릭 합니다.

![](./media/app-insights-javascript/37.png)


클릭 `...` Ajax 호출에 대 한 모든 원격 분석 hello에 대 한 합니다.

### <a name="no-ajax-calls-reported"></a>Ajax 호출이 보고되지 않았습니까?
Ajax 호출에서 웹 페이지의 hello 스크립트에서 HTTP/HTTPS 호출을 포함 합니다. 보고에 표시 되지 않으면 해당 hello 코드 조각 hello를 설정 하지 않습니다 확인 `disableAjaxTracking` 또는 `maxAjaxCallsPerView` [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)합니다.

## <a name="browser-exceptions"></a>브라우저 예외
Hello 브라우저 블레이드에는 예외 요약 차트 및 예외 형식의 추가 hello 블레이드 아래쪽 눈금입니다.

![](./media/app-insights-javascript/39.png)

브라우저 예외 보고 보이지 않으면 확인 해당 hello 코드 조각 설정 하지 않으므로 hello `disableExceptionTracking` [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)합니다.

## <a name="inspect-individual-page-view-events"></a>개별 페이지 보기 이벤트 검사

일반적으로 페이지 보기 원격 분석은 Application Insights에서 분석하며 모든 사용자에 대해 계산된 평균이 포함된 누적 보고서만 표시됩니다. 그러나 디버깅을 위해 개별 페이지 보기 이벤트를 확인할 수도 있습니다.

Hello 진단 검색 블레이드에서 필터 tooPage 보기를 설정 합니다.

![](./media/app-insights-javascript/12-search-pages.png)

모든 이벤트 toosee 자세히를 선택 합니다. Hello 세부 정보 페이지에서 "…" toosee 더 많은 세부 정보 클릭 합니다.

> [!NOTE]
> 사용 하는 경우 [검색](app-insights-diagnostic-search.md), 단어 단위로 toomatch 있다고 표시: "About" "에 대 한 내용은"와 "나타날 때" 일치 하지 않습니다.
> 
> 

사용할 수도 있습니다 hello 강력한 [로그 분석 쿼리 언어](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch 페이지 보기.

### <a name="page-view-properties"></a>페이지 보기 속성
* **페이지 보기 기간** 
  
  * 기본적으로 hello 하나 tooload hello 페이지 시간, 클라이언트 요청 toofull에서 (Ajax 호출 같은 비동기 작업을 제외 되지만 보조 파일 포함)를 로드 합니다. 
  * 설정한 경우 `overridePageViewDuration` hello에 [페이지 구성](#detailed-configuration), 클라이언트 요청 tooexecution hello의 간격을 먼저 hello `trackPageView`합니다. Hello 스크립트의 hello 초기화 된 후의 일반적인 위치에서 trackPageView를 이동한 경우 다른 값을 반영 됩니다.
  * 경우 `overridePageViewDuration` 설정 되 고 인수가 hello에 제공 되는 기간 `trackPageView()` 호출 hello 인수 값이 대신 사용 됩니다. 

## <a name="custom-page-counts"></a>사용자 지정 페이지 수
기본적으로 페이지 수는 hello 클라이언트 브라우저에 새 페이지가 로드 될 때마다 발생 합니다.  그러나 toocount 추가 페이지 뷰를 원할 수 있습니다. 예를 들어 페이지 탭에서 해당 콘텐츠를 표시할 수 있습니다 및 hello 사용자 탭 전환할 때 원하는 toocount 페이지입니다. 또는 hello 페이지에서 JavaScript 코드 hello 브라우저의 URL을 변경 하지 않고 새 콘텐츠를 로드할 수 있습니다.

클라이언트 코드에서 hello 적절 한 시점에 다음과 같은 JavaScript 호출을 삽입 합니다.

    appInsights.trackPageView(myPageName);

hello 페이지 이름에는 동일한 문자를 URL로 모든 항목 "#" 후 hello 포함 될 수 있습니다 또는 "?"는 무시 됩니다.

## <a name="usage-tracking"></a>사용 추적
응용 프로그램으로 수행할 사용자에 게 아웃 toofind를 선택 하십시오.

* [사용 추적에 대해 알아보기](app-insights-web-track-usage.md)
* [사용자 지정 이벤트 및 메트릭 API에 대해 자세히 알아보세요](app-insights-api-custom-events-metrics.md).

## <a name="video"></a>동영상


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> 다음 단계
* [사용 현황 추적](app-insights-web-track-usage.md)
* [사용자 지정 이벤트 및 메트릭](app-insights-api-custom-events-metrics.md)
* [빌드 - 측정 - 학습](app-insights-web-track-usage.md)


---
title: "aaa Azure Application Insights 란? | Microsoft Docs"
description: "라이브 웹 응용 프로그램의 응용 프로그램 성능을 관리하고 사용 현황을 추적합니다.  문제를 감지, 심사, 진단하고 사람들이 앱을 사용하는 방식을 이해합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a>Application Insights란?
Application Insights는 여러 플랫폼의 웹 개발자를 위한 확장 가능한 APM(응용 프로그램 성능 관리) 서비스입니다. Toomonitor를 사용 하 여 라이브 웹 응용 프로그램입니다. 성능 이상을 자동으로 감지합니다. Toounderstand 응용 프로그램과 함께 실제로 사용자가 수행 하 고 문제를 진단 하는 강력한 분석 도구 toohelp을 포함 됩니다.  기능은 toohelp 성능과 유용성 지속적으로 향상 됩니다. 앱에 대 한 작동.NET, Node.js 및 J2EE 포함 하는 플랫폼은 다양 한 온-프레미스 호스팅 또는 hello 클라우드에 있습니다. DevOps 프로세스와 통합 하 고에 연결 지점 tooa 다양 한 개발 도구입니다.

![사용자 활동 통계, 차트 또는 특정 이벤트를 드릴합니다.](./media/app-insights-overview/00-sample.png)

[Hello 소개 애니메이션 살펴보기](https://www.youtube.com/watch?v=fX2NtGrh-Y0)합니다.

## <a name="how-does-application-insights-work"></a>Application Insights의 작동 방식
응용 프로그램에서 작은 계측 패키지를 설치 하 고 hello Microsoft Azure 포털에는 Application Insights 리소스를 설정 합니다. hello 계측 응용 프로그램을 모니터링 하 고 원격 분석 데이터 toohello 포털을 보냅니다. (hello 응용 프로그램 원격 실행할 수-toobe Azure에서 호스트 되는 것은 아닙니다.)

Hello 웹 서비스 응용 프로그램 뿐 아니라 모든 백그라운드 구성 요소를 계측할 수 있으며 자체 hello 웹 페이지에서 JavaScript hello 수 있습니다. 

![응용 프로그램에서 응용 프로그램 Insights 계측으로 인 한 원격 분석 tooyour Application Insights 리소스를 보냅니다.](./media/app-insights-overview/01-scheme.png)


또한 성능 카운터, Azure 진단 또는 Docker 로그 같은 hello 호스트 환경에서 원격 분석에서 가져올 수 있습니다. 정기적으로 요청을 보내는 통합 tooyour 웹 서비스 웹 테스트를 설정할 수 있습니다.

이러한 원격 분석 스트림에에 통합 되어 모든 hello Azure 포털을 적용할 수 있는 강력한 분석 및 검색 도구 toohello 원시 데이터입니다.


### <a name="whats-hello-overhead"></a>Hello 오버 헤드는 무엇입니까?
앱의 성능에 미치는 영향 hello는 매우 작습니다. 추적 호출은 차단되지 않으며, 별도의 스레드로 일괄 처리 및 전송합니다.

## <a name="what-does-application-insights-monitor"></a>Application Insights는 무엇을 모니터링하나요?

Application Insights는 hello 개발 팀에서 앱이 수행 되는 방법 및 사용 되는 방식을 이해 toohelp 목표로 합니다. 다음 사항을 모니터링합니다.

* **요청 속도, 응답 시간 및 실패율** - 하루 중 어느 시간에 어떤 페이지를 가장 많이 방문하는지, 사용자가 어디에 있는지 확인합니다. 어떤 페이지가 가장 성능이 우수한지 확인합니다. 요청이 더 있는데 응답 시간과 실패율이 높아지면 아마도 리소스 문제가 있는 것입니다. 
* **종속성 비율, 응답 시간 및 실패율** - 외부 서비스 때문에 속도가 느려지는지 확인합니다.
* **예외** -hello 집계 통계를 분석 하거나 특정 인스턴스를 선택 하 고 hello 스택 추적 및 관련된 요청으로 드릴 합니다. 서버 및 브라우저 예외가 전부 보고됩니다.
* **페이지 보기 및 로드 성능** - 사용자의 브라우저에서 보고합니다.
* 웹 페이지의 **AJAX 호출** - 속도, 응답 시간 및 실패율.
* **사용자 및 세션 수**.
* Windows 또는 Linux 서버 컴퓨터의 **성능 카운터** - CPU, 메모리, 네트워크 사용량 등. 
* Docker 또는 Azure의 **호스트 진단**. 
* 앱의 **진단 추적 로그** - 추적 이벤트를 요청과 상호 연결하는 데 사용됩니다.
* **사용자 지정 이벤트 및 메트릭을** 는 사용자가 직접 작성 hello 클라이언트 또는 서버 코드에서 tootrack 비즈니스 이벤트 항목 판매 또는 획득 게임 등입니다.

## <a name="where-do-i-see-my-telemetry"></a>원격 분석은 어디서 찾을 수 있나요?

다양 한 방법으로 tooexplore 데이터입니다. 다음 문서를 확인하세요.

|  |  |
| --- | --- |
| [**스마트 검색 및 수동 경고**](app-insights-proactive-diagnostics.md)<br/>자동 경고 hello 일반 패턴 외부 대상이 있는 경우 원격 분석 및 트리거 tooyour 응용 프로그램의 일반 패턴을 활용 합니다. 특정 수준의 사용자 지정 또는 표준 메트릭에 대해 [경고를 설정](app-insights-alerts.md)할 수도 있습니다. |![경고 샘플](./media/app-insights-overview/alerts-tn.png) |
| [**응용 프로그램 맵**](app-insights-app-map.md)<br/>주요 메트릭 및 경고와 함께 응용 프로그램의 hello 구성 요소입니다. |![응용 프로그램 맵](./media/app-insights-overview/appmap-tn.png)  |
| [**프로파일러**](app-insights-profiler.md)<br/>샘플링 된 요청의 hello 실행 프로필을 검사 합니다. |![프로파일러](./media/app-insights-overview/profiler.png) |
| [**사용 현황 분석**](app-insights-usage-overview.md)<br/>사용자 구분 및 재방문 주기를 분석합니다.|![재방문 주기 도구](./media/app-insights-overview/retention.png) |
| [**인스턴스 데이터에 대한 진단 검색**](app-insights-diagnostic-search.md)<br/>요청, 예외, 종속성 호출, 로그 추적 및 페이지 보기와 같은 이벤트를 검색하고 필터링할 수 있습니다.  |![원격 분석 검색](./media/app-insights-overview/search-tn.png) |
| [**집계된 데이터에 대한 메트릭 탐색기**](app-insights-metrics-explorer.md)<br/>요청, 오류 및 예외의 비율과 응답 시간, 페이지 로드 시간과 같은 집계된 데이터를 탐색, 필터링 및 분할할 수 있습니다. |![메트릭](./media/app-insights-overview/metrics-tn.png) |
| [**대시보드**](app-insights-dashboards.md#dashboards)<br/>여러 리소스의 데이터를 매시업한 후 다른 사용자와 공유할 수 있습니다. 다중 구성 요소 응용 프로그램 및 hello 팀 대화방에 연속 표시에 유용 합니다. |![대시보드 샘플](./media/app-insights-overview/dashboard-tn.png) |
| [**라이브 메트릭 스트림**](app-insights-live-stream.md)<br/>새 빌드를 배포 하면 이러한 거의 실시간 성능 지표 toomake 있는지 예상 대로 작동 하는 것을 시청 합니다. |![라이브 메트릭 샘플](./media/app-insights-overview/live-metrics-tn.png) |
| [**분석**](app-insights-analytics.md)<br/>이 강력한 쿼리 언어를 사용하여 앱의 성능 및 사용 현황에 대한 까다로운 질문에 답변할 수 있습니다. |![분석 샘플](./media/app-insights-overview/analytics-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>Hello 코드의 성능 데이터를 참조 하십시오. 스택 추적에서 toocode를 이동 합니다.|![Visual studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**스냅숏 디버거**](app-insights-snapshot-debugger.md)<br/>실시간 작업에서 샘플링된 스냅숏을 매개 변수 값으로 디버그합니다.|![Visual studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>사용 현황 메트릭을 다른 비즈니스 인텔리전스와 통합합니다.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**REST API**](https://dev.applicationinsights.io/)<br/>메트릭 및 원시 데이터를 통해 코드 toorun 쿼리를 작성 합니다.| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [**연속 내보내기**](app-insights-export-telemetry.md)<br/>도착 하는 즉시 대량 원시 데이터 toostorage 내보냅니다. |![내보내기](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Application Insights를 어떻게 사용하나요?

### <a name="monitor"></a>모니터
앱에 Application Insights를 설치하고, [가용성 웹 테스트를 설정](app-insights-monitor-web-app-availability.md)하고, 다음을 수행합니다.

* 설정 된 [대시보드](app-insights-dashboards.md) 팀 대화방 부하, 응답 및 종속성의 hello 성능에 눈은 tookeep, 페이지 로드 및 AJAX 호출 합니다.
* 가장 느린 hello 되며 대부분의 실패 한 요청을 검색 합니다.
* 조사식 [라이브 스트림을](app-insights-live-stream.md) tooknow 저하 되는 방법에 대 한 즉시 새 릴리스를 배포 하는 경우.

### <a name="detect-diagnose"></a>감지, 진단
경고를 수신하거나 문제를 검색한 경우:

* 얼마나 많은 사용자가 영향을 받는지 평가합니다.
* 오류는 예외, 종속성 호출 및 추적과 연관이 있습니다.
* 프로파일러, 스냅숏, 스택 덤프 및 추적 로그를 검사합니다.

### <a name="build-measure-learn"></a>빌드, 측정, 학습
[Hello 효율성을 측정](app-insights-usage-overview.md) 배포 하는 각 새로운 기능입니다.

* Toomeasure 계획 고객 새 UX 또는 비즈니스 기능을 사용 하는 방법입니다.
* 코드에 사용자 지정 원격 분석을 작성합니다.
* 기본 hello 다음 개발에 대 한 하드 증명이 원격 분석에서 순환 합니다.

## <a name="get-started"></a>시작
Application Insights 원격 분석 및 Microsoft Azure 내에서 호스트 되는 많은 서비스 분석 및 프레젠테이션에 대 한 있습니다 보내집니다 hello 중 하나입니다. 까다롭기 때문에 다른 작업을 수행 하기 전에 구독을 너무[Microsoft Azure](http://azure.com)합니다. 무료 toosign 이며 선택 하는 경우 기본 hello [계획 가격 책정](https://azure.microsoft.com/pricing/details/application-insights/) Application insights는 무료 응용 프로그램 증가 toohave 상당한 사용 될 때까지 합니다. 구독을 조직에 이미 있으면, Microsoft 계정 tooit를 추가할 수 있습니다.

여러 가지 tooget 시작 합니다. 본인에게 적합한 방법으로 시작합니다. 나중에 다른 hello를 추가할 수 있습니다.

* **런타임에: hello 서버에 웹 응용 프로그램을 계측 합니다.** 모든 업데이트 toohello 코드를 방지할 수 있습니다. 관리자 액세스 tooyour 서버가 필요 합니다.
  * [**IIS 온-프레미스 또는 VM**](app-insights-monitor-performance-live-website-now.md)
  * [**Azure 웹앱 또는 VM**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **개발 시: Application Insights tooyour 코드를 추가 합니다.** Toowrite 사용자 지정 원격 분석 및 tooinstrument 백 엔드와 데스크톱 응용 프로그램을 있습니다.
  * [Visual Studio](app-insights-asp-net.md) 2013 업데이트 2 이상
  * [Eclipse](app-insights-java-eclipse.md)의 Java 또는 [기타 도구](app-insights-java-get-started.md)
  * [Node.JS](app-insights-nodejs.md)
  * [기타 플랫폼](app-insights-platforms.md)
* 페이지 보기, AJAX 및 기타 클라이언트 쪽 원격 분석에 대해 **[웹 페이지를 계측](app-insights-javascript.md)**합니다.
* **[가용성 테스트](app-insights-monitor-web-app-availability.md)** -서버에서 정기적으로 웹 사이트를 ping합니다.


## <a name="next-steps"></a>다음 단계
다음을 사용하여 런타임에 시작하세요.

* [IIS 서버](app-insights-monitor-performance-live-website-now.md)
* [J2EE 서버](app-insights-java-live.md)

다음을 사용하여 개발 시에 시작하세요.

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.JS](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>지원 및 피드백
* 질문 및 문제:
  * [문제 해결][qna]
  * [MSDN 포럼](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* 사용자 제안:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* 블로그:
  * [Application Insights 블로그](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>비디오

[![애니메이션 소개](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md

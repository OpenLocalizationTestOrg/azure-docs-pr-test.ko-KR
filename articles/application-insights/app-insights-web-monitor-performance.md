---
title: "aaaMonitor 응용 프로그램의 상태 및 Application Insights와 사용"
description: "Application Insights를 시작합니다. 온-프레미스 또는 Microsoft Azure 웹 응용 프로그램의 사용량, 가용성 및 성능을 분석합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>웹 응용 프로그램의 성능 모니터링


응용 프로그램이 정상적으로 작동하는지 확인하고 오류가 발생하는지 신속하게 파악합니다. [Application Insights] [ start] 모든 성능 문제 및 예외에 대해 알려 고 근본 원인을 찾아 hello 진단는 데 도움이 됩니다.

Application Insights에서 Java 및 ASP.NET 웹 응용 프로그램과 서비스, WCF 서비스를 모니터링할 수 있습니다. 온-프레미스, 가상 컴퓨터에서 또는 Microsoft Azure 웹 사이트로 호스트할 수 있습니다. 

Hello 클라이언트 쪽에서 Application Insights 웹 페이지 및 다양 한 iOS, Android 및 Windows 스토어 앱을 포함 하 여 장치에서 원격 분석을 걸릴 수 있습니다.

>[!Note]
> 웹 응용 프로그램에서 느리게 작동하는 페이지 찾기에 사용할 수 있는 새 환경을 만들었습니다. 액세스 tooit 없으면 hello로 미리 보기 옵션을 구성 하 여 활성화 [미리 보기 블레이드에서](app-insights-previews.md)합니다. 이 새로운 환경에 대 한 읽기 [찾아 여 hello 대화형 성능 조사 성능 병목 현상을 해결](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation)합니다.

## <a name="setup"></a>성능 모니터링 설정
Application Insights tooyour 아직 추가 하지 않은 경우 (즉, 없는 경우 ApplicationInsights.config) 프로젝트를 다음이 방법 중 하나를 선택 tooget 시작:

* [ASP.NET 웹 앱](app-insights-asp-net.md)
  * [예외 모니터링 추가](app-insights-asp-net-exceptions.md)
  * [종속성 모니터링 추가](app-insights-monitor-performance-live-website-now.md)
* [J2EE 웹앱](app-insights-java-get-started.md)
  * [종속성 모니터링 추가](app-insights-java-agent.md)

## <a name="view"></a>성능 메트릭 탐색
[Azure 포털 hello](https://portal.azure.com), 응용 프로그램에 대해 설정한 toohello Application Insights 리소스를 검색 합니다. hello 개요 블레이드에 기본 성능 데이터를 보여 줍니다.

더 긴 기간에 대 한 모든 차트 toosee toosee 결과 및 구체적으로 말하면를 클릭 합니다. 예를 들어 hello 요청 타일을 클릭 하 고 시간 범위를 선택 합니다.

![Toomore 데이터를 클릭 하 고 시간 범위를 선택 합니다.](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

차트 toochoose 메트릭을 표시 하 고, 또는 새 차트를 추가 하 고 해당 메트릭을 선택를 클릭 합니다.

![그래프 toochoose 메트릭 클릭](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **모든 hello 메트릭을 선택 취소** 사용할 수 있는 toosee hello 전체 선택 합니다. 그룹에 속합니다 hello 메트릭 그룹의 모든 구성원을 선택 하면만 hello 해당 그룹의 다른 멤버가 나타납니다.

## <a name="metrics"></a>성능 메트릭의 의미 성능 타일 및 보고서
다양한 성능 메트릭을 가져올 수 있습니다. 응용 프로그램 블레이드 hello에 기본적으로 표시 되는 것부터 시작 하겠습니다.

### <a name="requests"></a>요청
지정 된 기간 동안에서 받은 HTTP 요청의 hello 수입니다. 이 다른 보고서 toosee 앱이 동작 하는 hello 부하가 변경 됨에 대 한 hello 결과와 비교 합니다.

HTTP 요청에는 페이지, 데이터 및 이미지에 대한 모든 GET 또는 POST 요청이 포함됩니다.

특정 Url에 대 한 hello 타일 tooget 횟수에 클릭 합니다.

### <a name="average-response-time"></a>평균 응답 시간
입력 응용 프로그램 및 hello 응답 반환 되는 웹 요청 사이의 측정값 hello 시간입니다.

hello 포인트 표시는 이동 평균입니다. 많은 요청 인 있을 수 있습니다 일부는 확실 한 최고 없이 hello 평균 으로부터 파생할 또는 hello 그래프에 함.

요청 수의 비정상적인 증가를 확인합니다. 일반적으로 요청의 증가와 응답 시간 toorise가 있기만 하면 됩니다. Hello 상승 불균형 이면 응용 프로그램 사용 하 여 서비스의 CPU 또는 hello 용량 등 리소스 제한에 도달 될 수 있습니다.

특정 Url에 대 한 hello 타일 tooget 번 클릭 합니다.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>가장 느린 요청
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

성능 튜닝이 필요할 수 있는 요청을 표시합니다.

### <a name="failed-requests"></a>실패한 요청
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

catch되지 않은 예외를 throw한 요청의 수입니다.

Hello 타일 toosee hello 세부 정보 중에서 특정 오류를 클릭 하 고 개별 요청 toosee 해당 세부 정보를 선택 합니다. 

오류의 대표 샘플만 개별적으로 조사할 수 있도록 보관됩니다.

### <a name="other-metrics"></a>기타 메트릭
toosee 어떤 기타 메트릭을 표시, 그래프를 클릭 한 다음 집합 선택을 취소 모든 hello 메트릭 toosee hello 전체 사용할 수 있습니다. (I)를 클릭 toosee 각 메트릭 정의 합니다.

![모든 메트릭 toosee hello 전체 집합을 선택 취소](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

동일한 차트에 표시할 수 없는 다른 hello 모든 메트릭 비활성화 hello를 선택 합니다.

## <a name="set-alerts"></a>경고 설정
경고를 추가 하는 toobe 비정상적인 값이 모든 메트릭의 전자 메일 알림을 받습니다. Toosend hello 전자 메일 toohello 계정 관리자 또는 toospecific 전자 메일 주소를 선택할 수 있습니다.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Hello 하기 전에 hello 리소스 다른 속성을 설정 합니다. 성능 또는 사용 메트릭을에 tooset 경고를 발생 시킬 경우 hello webtest 리소스를 선택 하지 마십시오.

묻는 메시지가 tooenter hello 임계값 신중 하 게 toonote hello 단위 수입니다.

*Hello 추가 경고 단추를 나타나지 않습니다.* -읽기 전용으로 액세스할 수 있는 그룹 계정 toowhich 인가요? 계정 관리자에 게 확인 하십시오.

## <a name="diagnosis"></a>문제 진단
아래에는 성능 문제를 찾고 진단하기 위한 몇 가지 팁이 나와 있습니다.

* 설정 [웹 테스트] [ availability] toobe 웹 사이트가 작동이 중단 또는 잘못 또는 느리게 응답 하는 경우 경고를 표시 합니다. 
* 오류 또는 대 한 느린 응답은 관련된 tooload 다른 메트릭 toosee와 hello 요청 개수를 비교 합니다.
* [삽입 및 추적 문을 검색] [ diagnostic] 코드 toohelp에서 문제를 파악 합니다.
* [라이브 메트릭 스트림][livestream]을 사용하여 작업에서 웹앱을 모니터링합니다.
* .NET 응용 프로그램의 hello 상태를 캡처하고자 [스냅숏 디버거][snapshot]합니다.

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>대화형 성능 조사를 사용하여 성능 병목 현상 찾기 및 해결

Hello 새 Application Insights 대화형 성능 조사 toolocate 영역 웹 응용 프로그램의 전반적인 성능이 저하 되는 사용할 수 있습니다. 신속 하 게 저하 되 고 hello를 사용 하는 특정 페이지 수 [프로 파일링 도구](app-insights-profiler.md) toosee 이러한 페이지 간의 상관 관계 없는 경우.

### <a name="create-a-list-of-slow-performing-pages"></a>느리게 작동하는 페이지 목록 만들기 

성능 문제를 찾는 데 hello 첫 단계에는 tooget hello 느린 응답 페이지의 목록입니다. 아래 스크린샷과 hello hello 성능 블레이드 tooget 잠재적인 페이지 tooinvestigate 추가로 목록을 사용 하 여 보여 줍니다. 신속 하 게 보면이 페이지에서 했음을 채우라는 hello 응용 프로그램의 hello 응답 시간이 약 오후 6시 및 오후 10 시 약에서 다시. Hello GET 고객/세부 정보 작업 507.05 밀리초 중앙 응답 시간의 일부 장기 실행 작업을 했는지를 확인할 수 있습니다. 

![Application Insights 대화형 성능](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>특정 페이지에 대해 드릴다운

앱의 성능에 대한 스냅숏을 만든 후 느리게 작동하는 특정 작업에 대한 자세한 세부 정보를 얻을 수 있습니다. 아래와 같이 hello 목록 toosee hello 측면에서 모든 작업을 클릭 합니다. Hello 차트 hello 성능 종속성 기반 하는 경우 확인할 수 있습니다. 또한 다양 한 응답 시간 수의 사용자가 숙련 된 hello를 볼 수 있습니다. 

![Application insights 작업 블레이드](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>특정 기간에 대해 드릴다운

특정 시점으로, 시간 tooinvestigate 식별 한 후 hello hello 성능 채우라는 원인이 될 수 있는 특정 작업에 더욱 toolook 세부적입니다. 시간에 특정 지점을 클릭할 때 아래 그림과 같이 hello 페이지의 hello 세부 정보를 가져옵니다. Hello에서 아래 예제에서는 지정된 된 기간 동안 hello 서버 응답 코드 및 hello 작업 기간에 대해 나열 된 hello 작업을 볼 수 있습니다. Toosend 정보 tooyour 개발 팀이 필요한 경우 TFS 작업 항목을 열어에 대해 hello url을 사용할 수도 있습니다.

![Application Insights 시간 조각](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>특정 작업에 대해 드릴다운

특정 시점으로, 시간 tooinvestigate 식별 한 후 hello hello 성능 채우라는 원인이 될 수 있는 특정 작업에 더욱 toolook 세부적입니다. 아래와 같이 hello 연산의 hello toosee hello 정보를 목록에서 작업을 클릭 합니다. Hello 작업이 실패 하 고 Application Insights는 hello의 hello 세부 정보를 제공 하는 확인할 수 있습니다이 예에서 예외 hello 응용 프로그램에서 발생 했습니다. 다시, 이 블레이드에서 TFS 작업 항목을 쉽게 만들 수 있습니다.

![Application insights 작업 블레이드](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>다음 단계
[웹 테스트] [ availability] -웹 요청 보낸 tooyour 응용 프로그램 hello 전 세계에서 정기적으로 합니다.

[캡처 및 진단 추적을 검색할] [ diagnostic] -추적 호출 삽입 하 고 hello 결과 toopinpoint 문제를 조사 합니다.

[사용 현황 추적][usage] - 사용자의 응용 프로그램 사용 방식을 파악합니다.

[문제 해결][qna] - 질문과 대답



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md




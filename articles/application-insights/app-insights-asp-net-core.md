---
title: "ASP.NET Core 용 Application Insights aaaAzure | Microsoft Docs"
description: "응용 프로그램의 가용성, 성능 및 사용 현황을 모니터링합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>ASP.NET Core용 Application Insights
[Application Insights](app-insights-overview.md)를 사용하여 웹 응용 프로그램의 가용성, 성능 및 사용량을 모니터링할 수 있습니다. 와일드 카드 hello 성능과 hello에서 응용 프로그램의 효율성에 대 한 get hello 피드백을 통해 각 개발 수명 주기의 hello 디자인의 hello 방향에 대 한 선택 가능한 항목을 만들 수 있습니다.

![예제](./media/app-insights-asp-net-core/sample.png)

[Microsoft Azure](http://azure.com)를 구독해야 합니다. Microsoft 계정으로 로그인합니다. Windows, XBox Live 또는 기타 Microsoft 클라우드 서비스의 계정을 사용할 수 있습니다. 팀에서 조직 구독 tooAzure을 할 수 있습니다: hello 소유자 tooadd 요청 tooit Microsoft 계정을 사용 하 여 합니다.

## <a name="getting-started"></a>시작

* Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights 구성** 또는 **추가 > Application Insights**를 선택합니다. [자세히 알아봅니다](app-insights-asp-net.md).
* 이러한 메뉴 명령을 보이지 않으면 따라 hello [가져오는 수동 시작 가이드](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started)합니다. 보아야 toodo이 버전의 Visual Studio 2017 하기 전에 프로젝트를 만든 경우.

## <a name="using-application-insights"></a>Application Insights 사용
Hello에 로그인 [Microsoft Azure 포털](https://portal.azure.com)선택, **모든 리소스** 또는 **Application Insights**, 한 다음 앱 toomonitor 만든 hello 리소스를 선택 합니다.

별도의 브라우저 창에서 잠시 앱을 사용합니다. Hello Application Insights 차트에 표시 되는 데이터를 표시 됩니다. (Tooclick 새로 고침 할 수도 있습니다.) 개발하는 동안은 소량의 데이터만 표시되지만, 앱을 게시하고 많은 사용자가 확보되면 차트가 흥미로워집니다. 

hello 개요 페이지에는 주요 성능 차트가 표시: 서버 응답 시간, 페이지 로드 시간 및 실패 한 요청 수입니다. 더 많은 차트 및 데이터에는 모든 차트 toosee를 클릭 합니다.

뷰 hello 포털의 세 가지 주요 범주에 속합니다.

* [메트릭 탐색기](app-insights-metrics-explorer.md) 사용자가 직접 hello로 만든 메트릭 및 수, 응답 시간, 실패율, 또는 메트릭을 같은 테이블 및 그래프 표시 [API](app-insights-api-custom-events-metrics.md)합니다. 응용 프로그램 및 해당 사용자의 속성 값 tooget 하 여 hello 데이터 필터와 세그먼트입니다.
* [탐색기 검색](app-insights-diagnostic-search.md) 특정 요청, 예외, 로그 추적 또는 hello를 사용 하 여 사용자가 직접 만든 이벤트와 같은 개별 이벤트를 나열 [API](app-insights-api-custom-events-metrics.md)합니다. 필터링 hello 이벤트에서 검색 하 고 관련된 이벤트 tooinvestigate 문제 사이에서 이동 합니다.
* [분석](app-insights-analytics.md) 은 원격 분석에 대해 SQL 유사 쿼리를 실행할 수 있도록 하는 강력한 분석 및 진단 도구입니다.

## <a name="alerts"></a>경고
* 실패율 및 기타 메트릭의 비정상적인 변경 내용을 알려 주는 [사전 진단 경고](app-insights-proactive-diagnostics.md)를 자동으로 가져옵니다.
* 설정 [가용성 테스트](app-insights-monitor-web-app-availability.md) tootest 전세계, 위치 및 get에서 지속적으로 웹 사이트 테스트에 실패 하는 즉시 전자 메일로 보냅니다.
* 설정 [메트릭 경고](app-insights-monitor-web-app-availability.md) tooknow 응답 시간이 나 서로 다른 예외 속도 같은 메트릭을 외부 허용 한계를 이동 합니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>공개 소스
[읽고 게시할 toohello 코드](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>다음 단계
* [원격 분석 tooyour 웹 페이지 추가](app-insights-javascript.md) toomonitor 페이지 사용 현황 및 성능.
* [종속성을 모니터링](app-insights-asp-net-dependencies.md) toosee 경우 REST, SQL 또는 기타 외부 리소스 느려지는 있습니다.
* [Hello API를 사용 하 여](app-insights-api-custom-events-metrics.md) toosend 사용자 이벤트와 앱의 성능 및 사용 현황의 더 자세한 보기에 대 한 메트릭을 합니다.
* [가용성 테스트](app-insights-monitor-web-app-availability.md) hello 전 세계에서 지속적으로 응용 프로그램을 확인 합니다. 


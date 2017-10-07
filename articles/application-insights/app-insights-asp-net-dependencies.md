---
title: "aaaDependency Azure Application Insights에서 추적 | Microsoft Docs"
description: "Application Insights를 사용하여 온-프레미스 또는 Microsoft Azure 웹 응용 프로그램의 사용량, 가용성 및 성능을 분석합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Application Insights 설정: 종속성 추적
*종속성*은 앱에서 호출하는 외부 구성 요소로, 일반적으로 HTTP, 데이터베이스 또는 파일 시스템을 사용하여 호출되는 서비스입니다. [Application Insights](app-insights-overview.md)는 응용 프로그램이 종속성을 기다리는 시간과 종속성 호출에 실패하는 빈도를 측정합니다. 특정 호출을 조사할 수 있으며 toorequests는 예외와 연결할 수 있습니다.

![예제 차트](./media/app-insights-asp-net-dependencies/10-intro.png)

hello의 기본 종속성 모니터는 현재 호출 toothese 종류의 종속성을 보고합니다.

* 서버
  * SQL 데이터베이스
  * ASP.NET 웹 및 HTTP 기반 바인딩을 사용하는 WCF 서비스
  * 로컬 또는 원격 HTTP 호출
  * Azure Cosmos DB, 테이블, Blob Storage 및 큐
* 웹 페이지
  * AJAX 호출

모니터링은 선택한 방법과 관련된 [바이트 코드 계측](https://msdn.microsoft.com/library/z9z62c29.aspx)을 사용하여 작동합니다. 성능 오버 헤드가 최소화됩니다.

사용자 고유의 SDK toomonitor 둘 다 hello 클라이언트와 서버 코드에서 다른 종속성을 사용 하 여 호출 hello를 작성할 수도 있습니다 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)합니다.

## <a name="set-up-dependency-monitoring"></a>종속성 모니터링 설정
Hello 하 여 부분 종속성 정보를 자동으로 수집 [Application Insights SDK](app-insights-asp-net.md)합니다. tooget 전체 데이터 hello hello 호스트 서버에 대 한 적절 한 에이전트를 설치 합니다.

| 플랫폼 | 설치 |
| --- | --- |
| IIS 서버 |어느 [상태 모니터 서버에 설치](app-insights-monitor-performance-live-website-now.md) 또는 [응용 프로그램 too.NET framework 4.6 이상 업그레이드](http://go.microsoft.com/fwlink/?LinkId=528259) hello를 설치 하 고 [Application Insights SDK](app-insights-asp-net.md) 응용 프로그램에서 합니다. |
| Azure 웹앱 |웹 응용 프로그램 제어 패널에서 [웹 응용 프로그램 제어판에서 Application Insights 블레이드 열기 hello](app-insights-azure-web-apps.md) 메시지가 표시 되 면 설치를 선택 합니다. |
| Azure 클라우드 서비스 |[시작 작업 사용](app-insights-cloudservices.md) 또는 [.NET Framework 4.6+ 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>여기서 toofind 종속성 데이터
* [응용 프로그램 맵](#application-map): 앱과 인접 구성 요소 간의 종속성을 시각화합니다.
* [성능, 브라우저 및 실패 블레이드](#performance-and-blades): 서버 종속성 데이터를 표시합니다.
* [브라우저 블레이드](#ajax-calls): 사용자 브라우저에서의 AJAX 호출을 표시합니다.
* [클릭 하 여 느리거나 실패 한 요청에서](#diagnose-slow-requests) toocheck 해당 종속성 호출입니다.
* [분석](#analytics) 사용된 tooquery 종속성 데이터 일 수 있습니다.

## <a name="application-map"></a>응용 프로그램 맵
응용 프로그램 맵 hello 응용 프로그램 구성 요소 간의 시각 toodiscovering 종속성으로 동작합니다. 응용 프로그램에서 hello 원격 분석에서 자동으로 생성 됩니다. 이 예제 응용 프로그램 tootwo 외부 서비스 hello 브라우저 스크립트에서 AJAX 호출 및 hello 서버에서 REST 호출 보여줍니다.

![응용 프로그램 맵](./media/app-insights-asp-net-dependencies/08.png)

* **Hello 상자에서 이동할** toorelevant 종속성 및 기타 차트입니다.
* **Pin hello 지도** toohello [대시보드](app-insights-dashboards.md)여기서 완벽 하 게 작동 수 있습니다.

[자세히 알아봅니다](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>성능 및 실패 블레이드
hello 성능 블레이드 hello 서버 응용 프로그램에서 수행한 종속성 호출의 hello 기간을 표시 합니다. 호출별로 구분된 요약 차트와 테이블이 있습니다.

![성능 블레이드 종속성 차트](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

요약 차트 hello 또는 hello 테이블 항목 toosearch 원시 횟수 이러한 호출을 통해 여기를 클릭 합니다.

![종속성 호출 인스턴스](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**실패 수가** hello에 표시 되는 **오류** 블레이드입니다. 오류가는 hello 범위 200-399, 또는 알 수 없음에 있지 않은 모든 반환 코드입니다.

> [!NOTE]
> **100% 실패?** - 이는 부분 종속성 데이터만 가져옴을 의미할 수 있습니다. 너무 필요한[모니터링 적절 한 tooyour 플랫폼 종속성 설정](#set-up-dependency-monitoring)합니다.
>
>

## <a name="ajax-calls"></a>AJAX 호출
hello 브라우저 블레이드 hello 기간을 표시 및에서 호출에 AJAX의 실패율 [웹 페이지에서 JavaScript](app-insights-javascript.md)합니다. 이는 종속성으로 표시됩니다.

## <a name="diagnosis"></a> 느린 요청 진단
종속성 호출 hello와 연결 된 각 요청 이벤트, 예외 및 앱을 처리 하는 동안 추적 되는 다른 이벤트 hello 요청 합니다. 따라서 일부 요청이 잘못 수행 하는 경우에 종속성의 응답을 tooslow 때문 인지 알아볼 수 있습니다.

이에 대한 예제를 살펴보겠습니다.

### <a name="tracing-from-requests-toodependencies"></a>요청 toodependencies에서 추적
Hello 성능 블레이드를 열고 요청 hello 표를 확인 합니다.

![평균 및 개수가 포함된 요청 목록](./media/app-insights-asp-net-dependencies/02-reqs.png)

hello 최상위 매우 오래 걸리면 하나입니다. Hello 시간이 소요 된 위치 알 수 하는 경우를 살펴보겠습니다.

해당 행 toosee 개별 요청 이벤트를 클릭 합니다.

![요청 항목 목록](./media/app-insights-asp-net-dependencies/03-instances.png)

또한 하 고 toohello 원격 종속성 호출 관련된 toothis 요청 아래로 스크롤하여 모든 장기 실행 인스턴스 tooinspect를 클릭 합니다.

![호출 tooRemote 종속성 찾기, 비정상적인 기간을 식별 합니다.](./media/app-insights-asp-net-dependencies/04-dependencies.png)

대부분이이 요청 호출 tooa 로컬 서비스에 소요 된 시간의 hello 시간 서비스의 모양입니다.

자세한 내용은 해당 행 tooget를 선택 합니다.

![클릭 하 여 해당 원격 종속성 tooidentify hello 원인](./media/app-insights-asp-net-dependencies/05-detail.png)

이 hello 문제는 여기서 같습니다. म hello 문제 원인을 해결 한, 방금 이제 이유 호출 하는 시간이 걸리거나 너무 오래 아웃 toofind 필요 합니다.

### <a name="request-timeline"></a>요청 시간 표시 막대
다른 경우에는 특별히 긴 종속성 호출이 없습니다. 하지만 toohello 타임 라인 보기를 전환 하 여 았습니다 hello 지연 내부 처리에서 발생 한 위치:

![호출 tooRemote 종속성 찾기, 비정상적인 기간을 식별 합니다.](./media/app-insights-asp-net-dependencies/04-1.png)

즉 이유 코드 toosee 우리의 표시 해야 하므로 hello 첫 번째 종속성 호출 이후의 toobe 큰 간격 같습니다.

### <a name="profile-your-live-site"></a>라이브 사이트 프로파일링

어떠한 정보도 표시 hello 시간 흐름 방향은? hello [Application Insights 프로파일러](app-insights-profiler.md) tooyour 라이브 사이트를 호출 하 고 사용자 코드에서 함수를 표시 하는 HTTP 추적 hello 가장 긴 시간이 걸렸습니다.

## <a name="failed-requests"></a>실패한 요청
실패 한 요청 실패 한 호출 toodependencies와 연결 될 수도 있습니다. 다시, tootrack hello 문제를 통해 누르면 됩니다.

![Hello 실패 한 요청 차트를 클릭 합니다.](./media/app-insights-asp-net-dependencies/06-fail.png)

해당 연결 된 이벤트를 실패 한 요청 tooan 번째 클릭 합니다.

![Hello 인스턴스 tooget tooa의 서로 다른 뷰를 요청 유형을 클릭 한 다음 동일한 인스턴스에 hello를 tooget 예외 세부 정보를 클릭 합니다.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>분석
Hello에서 종속성을 추적할 수 있습니다 [로그 분석 쿼리 언어](https://docs.loganalytics.io/)합니다. 다음은 몇 가지 예제입니다.

* 실패한 종속성 호출을 찾습니다.

```

    dependencies | where success != "True" | take 10
```

* AJAX 호출을 찾습니다.

```

    dependencies | where client_Type == "Browser" | take 10
```

* 요청과 연관된 종속성 호출을 찾습니다.

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* 페이지 보기와 관련된 AJAX 호출을 찾습니다.

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>사용자 지정 종속성 추적
hello 표준 종속성 추적 모듈은 데이터베이스 및 REST Api와 같은 외부 종속성이 자동으로 검색 합니다. 그러나 몇 가지 추가 구성 요소 toobe에서에서 처리 하는 hello 동일한 경우가 방식으로 합니다.

종속성 정보를 보내는 코드를 작성할 수 동일 hello를 사용 하 여 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello 표준 모듈에 의해 사용 되는 합니다.

예를 들어 코드 어셈블리와 사용자가 직접 작성 하지 않은, 모든 hello 호출 tooit 시간 수를 빌드하면 tooyour 응답은 어떤 기여 아웃 toofind 시간이 됩니다. 사용 하 여 toohave hello Application Insights 종속성 차트에 표시 된이 데이터 보내기 `TrackDependency`합니다.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Tooswitch hello 표준 종속성 추적 모듈 해제 하려는 경우 제거에 hello 참조 tooDependencyTrackingTelemetryModule [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다.

## <a name="troubleshooting"></a>문제 해결
*종속성 성공 플래그는 항상 true 또는 false로 표시됩니다.*

*SQL 쿼리가 일부만 표시됩니다.*

* Toohello hello SDK의 최신 버전을 업그레이드 합니다. .NET 버전이 4.6 미만인 경우:
  * IIS 호스트: 설치 [Application Insights 에이전트](app-insights-monitor-performance-live-website-now.md) hello 호스트 서버에 있습니다.
  * Azure 웹 앱: 열기 Application Insights hello 웹 응용 프로그램 제어 패널의 탭 및 Application Insights를 설치 합니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>다음 단계
* [예외](app-insights-asp-net-exceptions.md)
* [사용자 및 페이지 데이터](app-insights-javascript.md)
* [Availability](app-insights-monitor-web-app-availability.md)

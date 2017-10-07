---
title: "Application Insights에서 카운터 aaaPerformance | Microsoft Docs"
description: "Application Insights에서 시스템 및 사용자 지정 .NET 성능 카운터를 모니터링합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Application Insights의 시스템 성능 카운터
Windows는 광범위한 [성능 카운터](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters)(예: CPU 점유율, 메모리, 디스크, 네트워크 사용량 등)를 제공합니다. 또한 직접 정의할 수도 있습니다. [Application Insights](app-insights-overview.md) 응용 프로그램에서 실행 중인 경우 IIS에서 온-프레미스 가상 컴퓨터 또는 호스트 toowhich 하면 이러한 성능 카운터에 대 한 관리 권한이 표시할 수 있습니다. hello 차트 hello 리소스 사용 가능한 tooyour 라이브 응용 프로그램을 나타내고 서버 인스턴스 간의 tooidentify 불균형된 부하의 활용 합니다.

서버 인스턴스에서 분할 하는 테이블을 포함 하는 hello 서버 블레이드 성능 카운터가 표시 됩니다.

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/counters-by-server-instance.png)

(성능 카운터는 Azure Web Apps에서 사용할 수 없습니다. 하 고 있지만 [Azure 진단 tooApplication Insights 보낼](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>카운터 보기
hello 서버 블레이드 성능 카운터의 기본 집합을 보여 줍니다. 

toosee 다른 카운터 hello 서버 블레이드의 hello 차트를 편집 하거나 새 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드 및 새 차트를 추가 합니다. 

차트를 편집할 때 hello 사용 가능한 카운터 메트릭을으로 나열 됩니다.

![Application Insights에서 보고하는 시스템 성능 카운터](./media/app-insights-performance-counters/choose-performance-counters.png)

toosee를 한 곳에서 가장 유용한 모든 차트 만들기는 [대시보드](app-insights-dashboards.md) tooit를 고정 하 고 있습니다.

## <a name="add-counters"></a>카운터 추가
원하는 hello 성능 카운터 메트릭 hello Application Insights SDK 웹 서버에서 수집 되지 않습니다 때문에 hello 목록에 표시 되지 않습니다. 구성할 수 있습니다 toodo 하므로 합니다.

1. 어떤 카운터는 hello 서버에서이 PowerShell 명령을 사용 하 여 서버에서 사용할 수를 확인 합니다.
   
    `Get-Counter -ListSet *`
   
    ([`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx) 참조)
2. ApplicationInsights.config를 엽니다.
   
   * Application Insights tooyour 응용 프로그램을 개발 하는 동안 추가한 경우 프로젝트에서 ApplicationInsights.config를 편집 하 고 다시 배포 tooyour 서버입니다.
   * 런타임에 상태 모니터 tooinstrument 웹 응용 프로그램을 사용 하는 경우 IIS에서 hello 응용 프로그램의 루트 디렉터리 hello에에서 ApplicationInsights.config를 찾습니다. 각 서버 인스턴스에서 해당 ApplicationInsights.config를 업데이트합니다.
3. Hello 성능 수집기 지시문을 편집 합니다.
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

표준 카운터 및 사용자가 직접 구현한 카운터를 모두 캡처할 수 있습니다. `\Objects\Processes`는 모든 Windows 시스템에서 사용할 수 있는 표준 카운터의 한 예입니다. `\Sales(photo)\# Items Sold`는 웹 서비스에서 구현할 수 있는 사용자 지정 카운터의 한 예입니다. 

hello 형식은 `\Category(instance)\Counter"`, 인스턴스가 없는 범주에 대 한 바로 또는 `\Category\Counter`합니다.

`ReportAs`일치 하지 않는 카운터 이름에 대 한 필요 `[a-zA-Z()/-_ \.]+` -hello 관계 집합에 없는 문자가 포함 되어, 즉: 편지, 대괄호, 슬래시, 하이픈, 밑줄, 공간, 둥근 점입니다.

인스턴스를 지정 하면 차원 "CounterInstanceName" hello의 메트릭을 보고 수집 될지 것입니다.

### <a name="collecting-performance-counters-in-code"></a>코드에서 성능 카운터 수집
toocollect 시스템 성능 카운터 및 tooApplication Insights 보내거나, 아래 hello 조각 조정할 수 있습니다.


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

작업을 수행할 수 있습니다 또는 동일한 작업을 만든 사용자 지정 메트릭 hello:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>분석에서의 성능 카운터
[분석](app-insights-analytics.md)에서 성능 카운터 보고서를 검색하고 표시할 수 있습니다.

hello **performanceCounters** 스키마는 hello 노출 `category`, `counter` 이름 및 `instance` 각 성능 카운터의 이름입니다.  각 응용 프로그램에 대 한 hello 원격 분석에서 해당 응용 프로그램에 대 한 hello 카운터에만 표시 됩니다. 예를 들어 toosee 어떤 카운터를 사용할 수 있습니다. 

![Application Insights 분석의 성능 카운터](./media/app-insights-performance-counters/analytics-performance-counters.png)

(Toohello 성능 카운터 인스턴스는 여기 '인스턴스', 역할이 나 서버 컴퓨터 인스턴스를 hello 하지 않습니다. hello 성능 카운터 인스턴스 이름은 일반적으로 분할 하 프로세서 시간 비율 등 카운터 hello 프로세스 또는 응용 프로그램의 hello 이름별 합니다.)

tooget hello 최근 기간을 통해 사용 가능한 메모리의 차트: 

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-performance-counters/analytics-available-memory.png)

마찬가지로 다른 원격 분석 **performanceCounters** 열도 `cloud_RoleInstance` hello 호스트 서버 인스턴스가 실행 되는 앱의 hello id를 나타내는입니다. 예를 들어 toocompare hello 응용 프로그램의 성능을 hello 서로 다른 컴퓨터에서: 

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET 및 Application Insights 개수
*Hello 예외 속도 예외 메트릭 hello 차이 무엇입니까?*

* *예외 속도* 는 시스템 성능 카운터입니다. hello CLR 모든 처리 하는 hello와 처리 되지 않은 예외를 throw 되 고 샘플링 간격의 hello 간격의 길이 hello hello 총 나눕니다를 계산 합니다. Application Insights SDK hello이이 결과 수집 하 고 toohello 포털 보냅니다.
* *예외* hello 개수 TrackException 보고서 hello 차트의 hello 샘플링 간격의 hello 포털에서 수신 합니다. Hello TrackException 코드에서 호출 하 고 모든 포함 되지 않으면을 작성 하 한 예외 처리에 포함 [처리 되지 않은 예외](app-insights-asp-net-exceptions.md)합니다. 

## <a name="alerts"></a>경고
수 다른 메트릭과 마찬가지로 [경고를 설정](app-insights-alerts.md) toowarn 성능 카운터 제한 외부 라인 여부를 지정 합니다. Hello 경고 블레이드를 열고 추가 클릭 합니다.

## <a name="next"></a>다음 단계
* [종속성 추적](app-insights-asp-net-dependencies.md)
* [예외 추적](app-insights-asp-net-exceptions.md)


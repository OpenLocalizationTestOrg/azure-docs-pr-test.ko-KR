---
title: "Application Insights에서 aaaExplore.NET 추적 로그"
description: "추적, NLog 또는 Log4Net을 사용하여 생성된 로그를 검색합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Application Insights에서 .NET 추적 로그 탐색
전송 로그 점이 NLog, log4Net 또는 System.Diagnostics.Trace ASP.NET 응용 프로그램에서 진단 추적을 위해 사용 하는 경우[Azure Application Insights][start], 탐색 하 고 수 있는 검색 해당 합니다. 로그를 다른 hello로 병합 될 원격 분석을 식별할 수 있도록 응용 프로그램에서 들어오는 hello 각 사용자 요청을 서비스와 관련 된 추적 및 상관 관계 다른 이벤트와 예외 보고서를 지정 합니다.

> [!NOTE]
> Hello 로그 캡처 모듈 필요 한가요? 타사 로거에 대한 유용한 어댑터지만 NLog, log4Net 또는 System.Diagnostics.Trace를 사용하지 않는 경우 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 를 직접 호출하는 것이 좋습니다.
>
>

## <a name="install-logging-on-your-app"></a>앱에 대한 로깅 설치
프로젝트에서 선택한 로깅 프레임워크를 설치합니다. 그러면 app.config 또는 web.config에 항목이 생성됩니다.

System.Diagnostics.Trace를 사용 하는 항목 tooweb.config tooadd가 필요 합니다.

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Application Insights toocollect 로그 구성
**[Application Insights tooyour 프로젝트 추가](app-insights-asp-net.md)**  하는 작업을 아직 수행 하지 않은 경우. 옵션 tooinclude hello 로그 수집기를 볼 수 있습니다.

또는 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하여 **Application Insights를 구성** 합니다. Hello 옵션을 너무 선택**추적 수집을 구성**합니다.

*Application Insights 메뉴 또는 로그 수집기 옵션이 없습니까?* [문제 해결](#troubleshooting)을 시도해 보세요.

## <a name="manual-installation"></a>수동 설치
프로젝트 형식 hello Application Insights 설치 관리자 (예를 들어 Windows 데스크톱 프로젝트)에서 지원 되지 않는 경우이 메서드를 사용 합니다.

1. Toouse log4Net 또는 NLog를 하려는 경우 프로젝트에 설치 합니다.
2. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
3. "Application Insights" 검색
4. 중 적절 한 패키지-hello를 선택 합니다.

   * Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace 호출)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource 이벤트)
   * Microsoft.ApplicationInsights.EtwListener (toocapture ETW 이벤트)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

hello NuGet 패키지는 hello 필요한 어셈블리를 설치 하 고 web.config 또는 app.config도 수정 합니다.

## <a name="insert-diagnostic-log-calls"></a>진단 로그 호출 삽입
System.Diagnostics.Trace를 사용하는 경우 일반적인 호출 방법은 다음과 같습니다.

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Log4net 또는 NLog를 원할 경우

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>EventSource 이벤트 사용
구성할 수 있습니다 [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 이벤트 전송 toobe tooApplication Insights로 추적 합니다. 먼저, hello 설치 `Microsoft.ApplicationInsights.EventSourceListener` NuGet 패키지 합니다. 다음 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

각 원본에 대 한 매개 변수 뒤 hello를 설정할 수 있습니다.
 * `Name`hello EventSource toocollect hello 이름을 지정합니다.
 * `Level`로깅 수준 toocollect hello를 지정 합니다. `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.
 * `Keywords`(선택 사항) 키워드 조합 toouse의 hello 정수 값을 지정합니다.

## <a name="using-diagnosticsource-events"></a>DiagnosticSource 이벤트 사용
구성할 수 있습니다 [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) 이벤트 전송 toobe tooApplication Insights로 추적 합니다. 먼저, hello 설치 [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 패키지 합니다. 다음 hello 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

원하는 tootrace, 각 DiagnosticSource에 대 한 hello로 항목을 추가 `Name` 특성 프로그램 DiagnosticSource의 toohello 이름을 설정 합니다.

## <a name="using-etw-events"></a>ETW 이벤트 사용
TooApplication Insights 추적으로 전송 하는 ETW 이벤트 toobe를 구성할 수 있습니다. 먼저, hello 설치 `Microsoft.ApplicationInsights.EtwCollector` NuGet 패키지 합니다. 다음 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.

> [!NOTE] 
> ETW 이벤트 hello 프로세스 호스팅 hello SDK "Performance Log Users" 또는 관리자의 구성원 인 id에서 실행 중인 경우에 수집할 수 있습니다.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

각 원본에 대 한 매개 변수 뒤 hello를 설정할 수 있습니다.
 * `ProviderName`hello ETW 공급자 toocollect hello 이름이입니다.
 * `ProviderGuid`대신 사용할 수 hello hello ETW 공급자 toocollect의 GUID를 지정 `ProviderName`합니다.
 * `Level`로깅 수준 toocollect hello를 설정 합니다. `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.
 * `Keywords`(선택 사항) 집합 hello 키워드 조합 toouse의 정수 값입니다.

## <a name="using-hello-trace-api-directly"></a>Hello 추적 API를 직접 사용 하 여
Hello Application Insights 추적 API를 직접 호출할 수 있습니다. 이 API를 사용 하는 hello 로깅 어댑터.

예:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

TrackTrace 경우의 이점은 hello 메시지에 상대적으로 긴 데이터를 지정할 수 있습니다. 예를 들어, POST 데이터를 인코딩할 수 있습니다.

또한, 심각도 수준 tooyour 메시지를 추가할 수 있습니다. 와 같은 다른 원격 분석 toohelp 필터 또는 다른 집합이 추적에 대 한 검색 사용할 수 있는 속성 값을 추가할 수 있습니다. 예:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

이 사용 하면에서 [검색][diagnostic], tooeasily tooa 특정 데이터베이스와 관련 된 특정 심각도 수준의 모든 hello 메시지를 필터링 합니다.

## <a name="explore-your-logs"></a>로그 탐색
디버그 모드에서 앱을 실행하거나 실시간으로 배포합니다.

응용 프로그램의 개요 블레이드에서 [hello Application Insights 포털][portal], 선택 [검색][diagnostic]합니다.

![Application Insights에서 검색 선택](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![검색](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

예를 들어 다음을 수행할 수 있습니다.

* 특정 속성이 있는 로그 추적 또는 항목을 필터링합니다.
* 특정 항목을 자세히 검사합니다.
* Toohello와 관련 된 다른 원격 분석 찾기 같은 사용자 요청 (즉,와 동일한를 hello OperationId)
* 이 페이지의 hello 구성 즐겨찾기로 저장

> [!NOTE]
> **샘플링** 이상에 대 한 ASP.NET 버전 2.0.0-beta3 hello Application Insights SDK를 사용 하는 응용 프로그램에서 많은 양의 데이터를 hello 적응 샘플링 기능이 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다. [샘플링에 대해 자세히 알아봅니다.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>다음 단계
[ASP.NET의 실패 및 예외 진단][exceptions]

[검색에 대한 자세한 정보][diagnostic].

## <a name="troubleshooting"></a>문제 해결
### <a name="how-do-i-do-this-for-java"></a>Java의 경우 이 작업을 어떻게 수행하나요?
사용 하 여 hello [Java 로그 어댑터](app-insights-java-trace-logs.md)합니다.

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Hello 프로젝트 상황에 맞는 메뉴에서 Application Insights 옵션이 없습니다.
* Application Insights 도구가 이 개발 컴퓨터에 설치되어 있는지 확인합니다. Visual Studio 메뉴 도구, 확장 및 업데이트에서 Application Insights 도구를 찾습니다. Hello 설치 됨 탭에 없으면 온라인 hello 탭을 열고 설치 합니다.
* Application Insights 도구에서 지원되지 않는 프로젝트 형식일 수 있습니다. [수동 설치](#manual-installation)를 사용합니다.

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Hello 구성 도구에서 로그 어댑터 옵션 없음
* 먼저 tooinstall hello 로깅 프레임 워크가 필요합니다.
* System.Diagnostics.Trace를 사용하는 경우 [`web.config`에서 구성](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx)했는지 확인합니다.
* Application Insights의 최신 버전 hello 있죠? Visual Studio에서 **도구** 메뉴 선택 **확장명 및 업데이트**, 및 열기 hello **업데이트** 탭 합니다. 개발자 분석 도구 중지 되지 않은 경우, 클릭 tooupdate 것입니다.

### <a name="emptykey"></a>"계측 키는 비워 둘 수 없습니다." 오류가 발생합니다.
Application Insights를 설치 하지 않고 어댑터 Nuget 패키지 로깅 hello 설치한 같습니다.

솔루션 탐색기에서 `ApplicationInsights.config` 를 마우스 오른쪽 단추로 클릭하고 **Application Insights 업데이트**를 선택합니다. TooAzure 안에 toosign 초대 하는 대화 상자를 얻을 수 및 Application Insights 리소스를 만들거나 기존 집합을 다시 사용 하거나 합니다. 이 경우 문제가 해결된 것입니다.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>추적을 진단 검색에서 확인할 수는 있지만 다른 이벤트를 hello 하지
경우에 따라 모든 hello 이벤트 및 요청 tooget hello 파이프라인을 통해 시간이 걸릴 수 있습니다.

### <a name="limits"></a>얼마나 많은 데이터가 보존되나요?
보관 되는 데이터 양을 hello 영향을 주는 몇 가지 요소입니다. Hello 참조 [제한](app-insights-api-custom-events-metrics.md#limits) hello 고객 이벤트 메트릭 페이지에 대 한 자세한 내용은의 섹션입니다. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>예상 hello 로그 항목 일부는 표시 되지 않는
이상에 대 한 ASP.NET 버전 2.0.0-beta3 hello Application Insights SDK를 사용 하는 응용 프로그램에서 많은 양의 데이터를 hello 적응 샘플링 기능이 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다. [샘플링에 대해 자세히 알아봅니다.](app-insights-sampling.md)

## <a name="add"></a>다음 단계
* [가용성 및 응답성 테스트 설정][availability]
* [문제 해결][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md

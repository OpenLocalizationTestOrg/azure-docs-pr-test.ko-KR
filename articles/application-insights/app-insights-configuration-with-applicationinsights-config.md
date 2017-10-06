---
title: "aaaApplicationInsights.config 참조-Azure | Microsoft Docs"
description: "데이터 수집 모듈을 사용하거나 사용하지 않도록 설정하고 성능 카운터 및 기타 매개 변수를 추가합니다."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>ApplicationInsights.config 또는.xml을 사용 하 여 hello Application Insights SDK를 구성
Application Insights.NET SDK hello NuGet 패키지의 번호로 구성 됩니다. [코어 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights) hello Application Insights 원격 분석 보내기 위한 hello API를 제공 합니다. [추가 패키지](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)는 해당 컨텍스트 및 응용 프로그램에서 원격 분석을 자동으로 추적하기 위해 원격 분석 *모듈* 및 *이니셜라이저*를 제공합니다. Hello 구성 파일을 조정 하 여 또는 원격 분석 모듈 및 이니셜라이저를 사용 하지 않도록 설정를 그 중 일부에 대 한 매개 변수를 설정 합니다.

hello 구성 파일의 이름은 `ApplicationInsights.config` 또는 `ApplicationInsights.xml`hello 유형의 응용 프로그램에 따라 합니다. Tooyour는 자동으로 추가 때 프로젝트 있습니다 [대부분 hello SDK의 버전을 설치][start]합니다. Tooa 웹 앱으로도 추가 됩니다 [상태 모니터는 IIS 서버에][redfield], hello Appplication 통찰력을 선택 하면 [Azure 웹 사이트 또는 VM에 대 한 확장](app-insights-azure-web-apps.md)합니다.

해당 하는 파일 toocontrol hello 하지 않으므로 [웹 페이지에는 SDK][client]합니다.

이 문서에서는 hello 섹션에에서 나와 있는 hello 구성 파일, SDK, hello의 hello 구성 요소를 제어 하는 방법 및 해당 구성 요소를 로드 하는 NuGet 패키지에 설명 합니다.

## <a name="telemetry-modules-aspnet"></a>원격 분석 모듈(ASP.NET)
각 원격 분석 모듈 특정 형식의 데이터를 수집 하 고 hello 코어 API toosend hello 데이터를 사용 합니다. hello 모듈 hello 필요한 선을 toohello.config 파일에 추가 하 여 다른 NuGet 패키지를으로 설치 됩니다.

각 모듈에 대 한 hello 구성 파일에는 노드입니다. 모듈의 경우, toodisable hello 노드를 삭제 하거나 주석으로 처리 합니다.

### <a name="dependency-tracking"></a>종속성 추적 
[종속성 추적](app-insights-asp-net-dependencies.md) toodatabases 및 외부 서비스 및 데이터베이스 응용 프로그램가 호출 하는 방법에 대 한 원격 분석 수집 합니다. tooallow IIS 서버에서이 모듈 toowork, 필요한 너무[상태 모니터 설치][redfield]합니다. toouse Azure 웹 앱 또는 Vm에서 [hello Application Insights 확장 선택](app-insights-azure-web-apps.md)합니다.

사용자 고유의 종속성 hello를 사용 하 여 코드 추적을 작성할 수도 있습니다 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)합니다.

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 패키지.

### <a name="performance-collector"></a>성능 수집기
IIS 설치에서 CPU, 메모리 및 네트워크 부하와 같은 [시스템 성능 카운터를 수집](app-insights-performance-counters.md)합니다. 사용자가 직접 설정한 성능 카운터를 포함 하는 카운터 toocollect를 지정할 수 있습니다.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 패키지.

### <a name="application-insights-diagnostics-telemetry"></a>Application Insights 진단 원격 분석
hello `DiagnosticsTelemetryModule` hello Application Insights 계측 코드 자체에서 오류를 보고 합니다. 예를 들어 hello 코드 성능 카운터에 액세스할 수 없는 경우 또는 경우는 `ITelemetryInitializer` 예외를 throw 합니다. Hello에이 모듈에서 추적 하는 추적 원격 분석 표시 [진단 검색][diagnostic]합니다. 진단 데이터 toodc.services.vsallin.net을 보냅니다.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지. 만이 패키지를 설치한 경우 hello ApplicationInsights.config 파일이 자동으로 생성 되지 않습니다.

### <a name="developer-mode"></a>개발자 모드
`DeveloperModeWithDebuggerAttachedTelemetryModule`강제로 hello Application Insights `TelemetryChannel` toosend 데이터에 즉시 사용 경우 디버거는 한 번에 하나의 원격 분석 항목 toohello 응용 프로그램 프로세스를 연결 합니다. 이렇게 하면 응용 프로그램 원격 분석을 추적 하는 경우 및 hello Application Insights 포털에 표시 되 면 hello hello 순간 사이의 시간 크기를 감소 합니다. CPU 및 네트워크 대역폭에 상당한 오버 헤드가 발생합니다.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지

### <a name="web-request-tracking"></a>웹 요청 추적
보고서 hello [응답 시간 및 결과 코드](app-insights-asp-net.md) 의 HTTP 요청입니다.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지

### <a name="exception-tracking"></a>예외 추적
`ExceptionTrackingTelemetryModule` 는 웹앱에서 처리되지 않은 예외를 추적합니다. [오류 및 예외][exceptions]를 참조하세요.

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - [관찰되지 않은 작업 예외](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)를 추적합니다.
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 작업자 역할, Windows 서비스 및 콘솔 응용 프로그램에 대한 처리되지 않은 예외를 추적합니다.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지.

### <a name="eventsource-tracking"></a>EventSource 추적
`EventSourceTelemetryModule`tooconfigure를 EventSource 이벤트 toobe tooApplication Insights 추적 파일로 보낼 수 있습니다. EventSource 이벤트 추적에 대한 자세한 내용은 [EventSource 이벤트 사용](app-insights-asp-net-trace-logs.md#using-eventsource-events)을 참조하세요.

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>ETW 이벤트 추적
`EtwCollectorTelemetryModule`ETW 공급자 toobe tooApplication Insights 추적 파일로 전송에서 tooconfigure 이벤트가 있습니다. ETW 이벤트 추적에 대한 자세한 내용은 [ETW 이벤트 사용](app-insights-asp-net-trace-logs.md#using-etw-events)을 참조하세요.

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
hello Microsoft.ApplicationInsights 패키지 제공 hello [API 핵심](https://msdn.microsoft.com/library/mt420197.aspx) hello SDK의 합니다. hello 다른 원격 분석 모듈을 사용 하 여이 및 수도 있습니다 [toodefine를 사용 하 여 사용자 고유의 원격 분석](app-insights-api-custom-events-metrics.md)합니다.

* ApplicationInsights.config에 항목이 없습니다.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지. 이 NuGet을 설치하면 .config 파일이 생성되지 않습니다.

## <a name="telemetry-channel"></a>원격 분석 채널
hello 원격 분석 채널에는 버퍼링 및 원격 분석 toohello Application Insights 서비스의 전송을 관리합니다.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`서비스에 대 한 hello 기본 채널입니다. 메모리에 데이터를 버퍼링합니다.
* `Microsoft.ApplicationInsights.PersistenceChannel` 는 콘솔 응용 프로그램에 대한 대안입니다. 앱을 다운 닫고 hello 앱이 다시 시작 될 때 전송 합니다 어떤 unflushed 데이터 toopersistent 저장소를 절약할 수 있습니다.

## <a name="telemetry-initializers-aspnet"></a>원격 분석 이니셜라이저(ASP.NET)
원격 분석 이니셜라이저는 원격 분석의 모든 항목과 함께 전송되는 컨텍스트 속성을 설정합니다.

할 수 있습니다 [직접 이니셜라이저 작성](app-insights-api-filtering-sampling.md#add-properties) tooset 컨텍스트 속성입니다.

hello 표준 이니셜라이저 모두 설정 되었습니다. 하거나 hello 웹 또는 windows Server NuGet 패키지:

* `AccountIdTelemetryInitializer`hello AccountId 속성을 설정합니다.
* `AuthenticatedUserIdTelemetryInitializer`JavaScript SDK hello 여 세트로 hello AuthenticatedUserId 속성을 설정 합니다.
* `AzureRoleEnvironmentTelemetryInitializer`업데이트 hello `RoleName` 및 `RoleInstance` hello의 속성 `Device` hello Azure 런타임 환경에서 추출한 정보로 모든 원격 분석 항목에 대 한 컨텍스트입니다.
* `BuildInfoConfigComponentVersionTelemetryInitializer`업데이트 hello `Version` hello 속성 `Component` hello에서 추출한 hello 값으로 모든 원격 분석 항목에 대 한 컨텍스트 `BuildInfo.config` 파일이 하기 위해 Msbuild에 의해 생성 됩니다.
* `ClientIpHeaderTelemetryInitializer`업데이트 `Ip` hello 속성 `Location` hello에 따라 모든 원격 분석 항목의 상황에 맞는 `X-Forwarded-For` hello 요청의 HTTP 헤더입니다.
* `DeviceTelemetryInitializer`다음과 같은 hello의 속성 업데이트 hello `Device` 모든 원격 분석 항목에 대 한 컨텍스트입니다.
  * `Type`너무 설정 된 "PC"
  * `Id`hello 웹 응용 프로그램이 실행 되 고 있는 hello 컴퓨터의 toohello 도메인 이름을 설정 합니다.
  * `OemName`hello에서 추출 된 toohello 값으로 설정 되어 `Win32_ComputerSystem.Manufacturer` WMI를 사용 하 여 필드입니다.
  * `Model`hello에서 추출 된 toohello 값으로 설정 되어 `Win32_ComputerSystem.Model` WMI를 사용 하 여 필드입니다.
  * `NetworkType`hello에서 추출 된 toohello 값으로 설정 되어 `NetworkInterface`합니다.
  * `Language`hello toohello 이름이 설정 되어 `CurrentCulture`합니다.
* `DomainNameRoleInstanceTelemetryInitializer`업데이트 hello `RoleInstance` hello 속성 `Device` hello 웹 응용 프로그램을 실행 중인 hello 컴퓨터의 hello 도메인 이름의 모든 원격 분석 항목에 대 한 컨텍스트입니다.
* `OperationNameTelemetryInitializer`업데이트 hello `Name` hello 속성 `RequestTelemetry` 및 hello `Name` hello 속성 `Operation` hello HTTP 메서드: ASP.NET MVC 컨트롤러 및 작업 호출 된 tooprocess hello의 이름에 따라 모든 원격 분석 항목의 컨텍스트 요청입니다.
* `OperationIdTelemetryInitializer`또는 `OperationCorrelationTelemetryInitializer` 업데이트 hello `Operation.Id` 모든 원격 분석 항목의 컨텍스트 속성이 자동으로 생성 하는 hello로 요청을 처리 하는 동안 추적 `RequestTelemetry.Id`합니다.
* `SessionTelemetryInitializer`업데이트 hello `Id` hello 속성 `Session` hello에서 추출 된 값을 가진 모든 원격 분석 항목에 대 한 컨텍스트 `ai_session` hello 사용자의 브라우저에서 실행 되는 ApplicationInsights JavaScript 계측 코드 hello 하 여 생성 된 쿠키입니다.
* `SyntheticTelemetryInitializer`또는 `SyntheticUserAgentTelemetryInitializer` 업데이트 hello `User`, `Session` 및 `Operation` 가용성 테스트 또는 엔진 bot 검색 같은 통합 소스에서 요청을 처리 하는 경우 모든 원격 분석 항목의 컨텍스트 속성을 추적 합니다. 기본적으로 [메트릭 탐색기](app-insights-metrics-explorer.md) 는 가상 원격 분석을 표시하지 않습니다.

    hello `<Filters>` 설정 hello 요청의 속성을 식별 합니다.
* `UserAgentTelemetryInitializer`업데이트 hello `UserAgent` hello 속성 `User` hello에 따라 모든 원격 분석 항목의 상황에 맞는 `User-Agent` hello 요청의 HTTP 헤더입니다.
* `UserTelemetryInitializer`업데이트 hello `Id` 및 `AcquisitionDate` 의 속성 `User` hello에서 추출 된 값이 포함 된 모든 원격 분석 항목에 대 한 컨텍스트 `ai_user` hello hello 실행 되는 Application Insights JavaScript 계측 코드에 의해 생성 된 쿠키 사용자의 브라우저입니다.
* `WebTestTelemetryInitializer`HTTP 요청에서 제공 하는 대 한 사용자 id, 세션 id 및 가상 원본 속성 설정 hello [가용성 테스트](app-insights-monitor-web-app-availability.md)합니다.
  hello `<Filters>` 설정 hello 요청의 속성을 식별 합니다.

서비스 패브릭에서 실행 되는.NET 응용 프로그램에 대 한 hello를 포함할 수 있습니다 `Microsoft.ApplicationInsights.ServiceFabric` NuGet 패키지 합니다. 이 패키지에는 `FabricTelemetryInitializer`, 서비스 패브릭 속성 tootelemetry 항목을 추가 합니다. 자세한 내용은 참조 hello [GitHub 페이지](https://go.microsoft.com/fwlink/?linkid=848457) 이 NuGet 패키지에서 추가 된 hello 속성에 대 한 합니다.

## <a name="telemetry-processors-aspnet"></a>원격 분석 프로세서(ASP.NET)
원격 분석 프로세서 필터링 하 고 hello SDK toohello 포털에서 보내기 바로 전에 각 원격 분석 항목을 수정할 수 있습니다.

[고유한 원격 분석 프로세서를 작성](app-insights-api-filtering-sampling.md#filtering)할 수 있습니다.

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>적응 샘플링 원격 분석 프로세서(2.0.0-beta3부터)
이 옵션은 기본적으로 사용하도록 설정되어 있습니다. 앱에서 다양한 원격 분석을 보내는 경우 이 프로세서는 일부 정보를 제거합니다.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

알고리즘 hello hello 대상 시도 tooachieve hello 매개 변수를 제공 합니다. 각 인스턴스의 hello SDK 작업 하지 독립적으로 하므로 hello 실제 양의 원격 분석을 적절 하 게 곱합니다 서버가 여러 대의 컴퓨터의 클러스터 이면 합니다.

[샘플링에 대해 자세히 알아봅니다](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>고정 비율 샘플링 원격 분석 프로세서(2.0.0-beta1부터)
또한 표준 [샘플링 원격 분석 프로세서](app-insights-api-filtering-sampling.md) 도 있습니다(2.0.1부터).

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>채널 매개 변수(Java)
이러한 매개 변수는 hello Java SDK 해야 저장 방법과 플러시 hello 원격 분석 데이터를 수집 하는 영향을 줍니다.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
hello hello SDK의 메모리 내 저장소에 저장 될 수 있는 원격 분석 항목 수입니다. 이 수에 도달 하면 hello 원격 분석 버퍼 플러시-즉, 원격 분석 항목 hello toohello Application Insights 서버 보냅니다.

* 최소: 1
* 최대: 1000
* 기본값: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
얼마나 자주 hello hello 메모리 내 저장소에 저장 된 데이터는 결정 플러시된 (보낸된 tooApplication Insights) 합니다.

* 최소: 1
* 최대: 300
* 기본값: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Hello mb toohello 영구 저장소 hello 로컬 디스크에 할당 된 최대 크기를 결정 합니다. 이 저장소에 실패 한 클라이언트 전송 toobe toohello Application Insights 끝점 유지 원격 분석 항목에 사용 됩니다. Hello 저장소 크기를 충족 하는 경우 새 원격 분석 항목 무시 됩니다.

* 최소: 1
* 최대: 100
* 기본값: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
데이터를 표시 하는 hello Application Insights 리소스를 결정 합니다. 일반적으로 각 응용 프로그램에 대해 별도 키를 사용하여 별도 리소스를 만듭니다.

하려면 tooset hello 키 동적으로-예를 들어 응용 프로그램 toodifferent 리소스-에서 toosend 결과 찾으려는 경우 hello 구성 파일에서 hello 키를 생략 하 고 대신 코드에서 설정할 수 있습니다.

TelemetryConfiguration.Active hello 키를 설정 하는 표준 원격 분석 모듈을 포함 하 여 TelemetryClient의 모든 인스턴스에 대해 tooset hello 키. ASP.NET 서비스의 global.aspx.cs와 같은 초기화 메서드에 키를 설정합니다.

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Toosend 원하는 이벤트 tooa 다른 리소스의 특정 집합이 이벤트를 특정 TelemetryClient에 대 한 hello 키를 설정할 수 있습니다.

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

새 키를 tooget [hello Application Insights 포털에서 새 리소스 만들기][new]합니다.

## <a name="next-steps"></a>다음 단계
[Hello API에 대 한 자세한][api]합니다.

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

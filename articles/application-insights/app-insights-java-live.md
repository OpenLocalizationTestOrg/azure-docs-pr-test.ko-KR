---
title: "aaaApplication Java 용 Insights 웹 이미 사용 중인 라이브 앱"
description: "서버에서 이미 실행 중인 웹 응용 프로그램 모니터링 시작"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>이미 라이브 상태인 Java 웹앱용 Application Insights


J2EE 서버에서 이미 실행 되는 웹 응용 프로그램의 경우 사용 하 여 모니터링을 시작할 수 있습니다 [Application Insights](app-insights-overview.md) hello 없이 toomake 코드 변경 내용과 하거나 프로젝트를 다시 컴파일해야 합니다. 이 옵션을 tooyour 서버, 처리 되지 않은 예외 및 성능 카운터 전송 된 HTTP 요청에 대 한 정보를 가져옵니다.

해야 구독 너무[Microsoft Azure](https://azure.com)합니다.

> [!NOTE]
> 이 페이지에 hello 프로시저 실행 시 hello SDK tooyour 웹 응용 프로그램을 추가합니다. 이 런타임 계측 tooupdate 하거나 소스 코드를 다시 작성 하지 않는 경우에 유용 합니다. 가능 하면 권장 하지만 [hello SDK toohello 소스 코드 추가](app-insights-java-get-started.md) 대신 합니다. 코드 tootrack 사용자 활동을 작성 하는 등 추가 옵션을 제공 합니다.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Application Insights 계측 키 가져오기
1. Toohello 로그인 [Microsoft Azure 포털](https://portal.azure.com)
2. 새 Application Insights 리소스를 만들고 hello 응용 프로그램 종류 tooJava 웹 응용 프로그램을 설정 합니다.
   
    ![이름을 채우고 Java 웹 앱을 선택하여 만들기 클릭](./media/app-insights-java-live/02-create.png)

    hello 리소스가 몇 초 후에 생성 됩니다.

4. Hello 새 리소스를 열고 해당 계측 키를 가져옵니다. 해야 toopaste이이 키를 코드 프로젝트에 곧 합니다.
   
    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Hello SDK 다운로드
1. Hello 다운로드 [Java 용 Application Insights SDK](https://aka.ms/aijavasdk)합니다. 
2. 서버에서 hello SDK 내용 toohello 디렉터리 프로젝트 이진 파일은 추출 합니다. Tomcat을 사용하는 경우 이 디렉터리는 일반적으로 `webapps/<your_app_name>/WEB-INF/lib`에 위치합니다.

된다고 toorepeat이 각 서버 인스턴스 및 각 응용 프로그램에 대 한 참고 합니다.

## <a name="3-add-an-application-insights-xml-file"></a>3. Application Insights xml 파일 추가
ApplicationInsights.xml hello SDK를 추가한 hello 폴더에 만듭니다. 것에 다음 XML hello 합니다.

Hello Azure 포털에서에서 가져온 hello 계측 키를 대체 합니다.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* hello 계측 키 원격 분석의 모든 항목이 함께 전송 되 고 Application Insights toodisplay 지시, 리소스에 해당 합니다.
* hello HTTP 요청 구성 요소는 선택 사항입니다. 자동으로 요청 및 응답 시간 toohello 포털에 대 한 원격 분석을 보냅니다.
* 상관 관계 이벤트는 또한 toohello HTTP 요청 구성 요소입니다. Hello 서버에서 수신 하는 식별자 tooeach 요청이 할당 hello 속성 'Operation.Id'로 원격 분석의 속성 tooevery 항목으로이 식별자를 추가 합니다. Toocorrelate hello 원격 분석에서 필터를 설정 하 여 연결 된 각 요청 허용 [진단 검색](app-insights-diagnostic-search.md)합니다.

## <a name="4-add-an-http-filter"></a>4. HTTP 필터 추가
찾아 프로젝트 및 응용 프로그램 필터 구성 된 hello 웹 응용 프로그램 노드 아래 코드의 코드 조각은 다음 병합 hello에 hello web.xml 파일을 엽니다.

다른 모든 필터 전에 tooget hello 가장 정확한 결과 hello 필터 매핑되어야 합니다.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a>5. 방화벽 예외를 확인합니다.
너무 해야[toosend 나가는 데이터 예외를 설정할](app-insights-ip-addresses.md)합니다.

## <a name="6-restart-your-web-app"></a>6. 웹앱을 다시 시작합니다.
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Application Insights에서 원격 분석 보기
tooyour Application Insights 리소스 반환 [Microsoft Azure 포털](https://portal.azure.com)합니다.

HTTP 요청에 대 한 원격 분석 개요 블레이드에 hello에 나타납니다. (없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)

![샘플 데이터](./media/app-insights-java-live/5-results.png)

클릭 하 여 더 자세한 메트릭을 통해 모든 차트 toosee 합니다. 

![](./media/app-insights-java-live/6-barchart.png)

요청 hello 속성을 볼 때 요청 및 예외와 같은 연관 된 hello 원격 분석 이벤트를 볼 수 있습니다.

![](./media/app-insights-java-live/7-instance.png)

[메트릭에 대해 자세히 알아봅니다.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>다음 단계
* [원격 분석 tooyour 웹 페이지 추가](app-insights-javascript.md) 뷰와 사용자 메트릭을 toomonitor 페이지입니다.
* [웹 테스트 설정](app-insights-monitor-web-app-availability.md) toomake 라이브 및 응답성이 뛰어난 응용 프로그램 없이 계속 합니다.
* [로그 추적 캡처](app-insights-java-trace-logs.md)
* [이벤트 및 로그를 검색할](app-insights-diagnostic-search.md) toohelp 문제를 진단 합니다.


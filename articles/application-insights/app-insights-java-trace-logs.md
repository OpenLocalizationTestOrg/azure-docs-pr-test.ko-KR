---
title: "Azure Application Insights에서 로그 aaaExplore Java 추적 | Microsoft Docs"
description: "Application Insights에서 검색 Log4J 또는 Logback 추적 검색"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a>Application Insights에서 Java 추적 로그 탐색
Log4J 또는 Logback을 사용 중인 경우 (v 1.2 또는 v2.0) 추적을 위한 tooApplication Insights 탐색 하 고 검색 하 수를 자동으로 전송 하 여 추적 로그를 사용할 수 있습니다.

## <a name="install-hello-java-sdk"></a>Hello Java SDK 설치

아직 수행하지 않은 경우 [Java용 Application Insights SDK][java]를 설치합니다.

(대부분의 hello.xml 구성 파일을 생략할 수 있습니다 하지만 hello 이상 포함 해야, tootrack HTTP 요청 하지 않으려는 경우 `InstrumentationKey` 요소입니다. 또한를 호출 해야 `new TelemetryClient()` tooinitialize hello SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>로깅 라이브러리 tooyour 프로젝트 추가
*프로젝트에 대 한 적절 한 방법으로 hello를 선택 합니다.*

#### <a name="if-youre-using-maven"></a>Maven을 사용하는 경우...
Toouse Maven 빌드에 대 한 프로젝트에 이미 설치 되 면 hello 코드 조각을 pom.xml 파일에 다음 중 하나를 병합 합니다.

그런 다음 hello 프로젝트 종속성을 tooget hello 다운로드 된 이진 파일을 새로 고칩니다.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Gradle을 사용하는 경우...
Hello 줄 toohello 다음 중 하나를 toouse Gradle 빌드에 대 한 프로젝트에 이미 설치 되 면 하는 경우 추가 `dependencies` 그룹의 build.gradle 파일이에서:

그런 다음 hello 프로젝트 종속성을 tooget hello 다운로드 된 이진 파일을 새로 고칩니다.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>기타...
다운로드 하 고 적절 한 hello 어 펜더를 추출 한 다음 hello 적절 한 라이브러리 tooyour 프로젝트 추가:

| 로거 | 다운로드 | 라이브러리 |
| --- | --- | --- |
| Logback |[Logback 어펜더를 사용한 SDK](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[Log4J v2 어펜더를 사용한 SDK](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[Log4J v1.2 어펜더를 사용한 SDK](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Hello 어 펜더 tooyour 로깅 프레임 워크 추가
추적, 코드 toohello Log4J 또는 Logback 구성 파일의 병합 hello 관련 조각을 toostart: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

hello Application Insights 어 펜더가 제공 (위의 hello 코드 샘플에 표시)으로 구성 된 모든로 거를 여는 것 뿐 아니라 hello 루트 로거에서 참조할 수 있습니다.

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Hello Application Insights 포털에서 사용자 추적 탐색
구성한 경우 했으므로 프로젝트 toosend tooApplication Insights 추적, 확인 및 hello에 hello Application Insights 포털에서 이러한 추적을 검색할 수 있습니다 [검색] [ diagnostic] 블레이드입니다.

![Hello Application Insights 포털에서 검색 시작](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>다음 단계
[진단 검색][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md



---
title: "aaaPerformance Azure Application Insights에서 Java 웹 앱에 대 한 모니터링 | Microsoft Docs"
description: "Application Insights로 Java 웹 사이트의 확장된 성능 및 사용량 모니터링"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>종속성, 예외 및 Java 웹앱에서의 실행 시간을 모니터링합니다.


있는 경우 [Java 웹 앱을 Application Insights 계측][java], hello Java 에이전트 tooget 심층적인 통찰력, 코드 변경 없이 사용할 수 있습니다.

* **종속성:** 응용 프로그램에서 tooother 구성 요소를 포함 하는 호출에 대 한 데이터:
  * **REST 호출** .
  * **Redis** hello Jedis 클라이언트를 통해 수행 된 호출 합니다. Hello 호출 단위: 10 보다 더 오래 걸리면, hello 에이전트는 또한 hello 호출 인수를 인출 합니다.
  * **[JDBC 호출](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB 또는 Apache Derby DB "executeBatch"호출이 지원됩니다. MySQL 및 PostgreSQL hello 호출 단위: 10, 보다 오래 걸리는 경우 hello 에이전트 hello 쿼리 계획을 보고 합니다.
* **예외 포착:** 코드에서 처리하는 예외에 대한 데이터입니다.
* **메서드 실행 시간:** 것 hello에 대 한 데이터는 tooexecute 특정 메서드를 제공 하는 시간입니다.

toouse hello Java 에이전트에 설치한 서버입니다. 웹 앱으로 hello로 계측 해야 [Application Insights Java SDK][java]합니다. 

## <a name="install-hello-application-insights-agent-for-java"></a>Java 용 Application Insights 에이전트 hello 설치
1. Hello 컴퓨터에서 Java 서버에서 실행 [hello 에이전트 다운로드](https://aka.ms/aijavasdk)합니다.
2. Hello 응용 프로그램 서버 시작 스크립트를 편집 하 고 다음 JVM hello 추가:
   
    `javaagent:`*전체 경로 toohello 에이전트 JAR 파일*
   
    예를 들어 Linux 컴퓨터의 Tomcat에서:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. 응용 프로그램 서버를 다시 시작합니다.

## <a name="configure-hello-agent"></a>Hello 에이전트 구성
라는 파일을 만들어 `AI-Agent.xml` hello에 넣는 hello 에이전트 JAR 파일과 같은 폴더입니다.

Hello xml 인의 hello 콘텐츠를 설정 합니다. 다음 예제에서는 tooinclude hello를 편집 하거나 원하는 hello 기능을 생략 합니다.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

Tooenable 보고서 예외 및 개별 메서드에 대 한 메서드 타이밍 해야합니다.

기본적으로 `reportExecutionTime`은 true이고 `reportCaughtExceptions`는 false입니다.

## <a name="view-hello-data"></a>Hello 데이터 보기
Application Insights 리소스 hello, 집계 된 원격 종속성과 메서드 실행 시간 표시 [hello 성능에서 타일][metrics]합니다.

종속성, 예외 및 메서드가 보고서의 개별 인스턴스에 대 한 toosearch 열고 [검색][diagnostic]합니다.

[종속성 문제 진단 - 자세한 내용](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>질문이 있으십니까? 문제가 있습니까?
* 데이터가 없나요? [방화벽 예외 설정](app-insights-ip-addresses.md)
* [Java 문제 해결](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md

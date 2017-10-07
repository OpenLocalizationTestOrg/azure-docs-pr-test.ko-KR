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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="f0ed2-103">종속성, 예외 및 Java 웹앱에서의 실행 시간을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="f0ed2-104">있는 경우 [Java 웹 앱을 Application Insights 계측][java], hello Java 에이전트 tooget 심층적인 통찰력, 코드 변경 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="f0ed2-105">**종속성:** 응용 프로그램에서 tooother 구성 요소를 포함 하는 호출에 대 한 데이터:</span><span class="sxs-lookup"><span data-stu-id="f0ed2-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="f0ed2-106">**REST 호출** .</span><span class="sxs-lookup"><span data-stu-id="f0ed2-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="f0ed2-107">**Redis** hello Jedis 클라이언트를 통해 수행 된 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="f0ed2-108">Hello 호출 단위: 10 보다 더 오래 걸리면, hello 에이전트는 또한 hello 호출 인수를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="f0ed2-109">**[JDBC 호출](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB 또는 Apache Derby DB</span><span class="sxs-lookup"><span data-stu-id="f0ed2-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="f0ed2-110">"executeBatch"호출이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="f0ed2-111">MySQL 및 PostgreSQL hello 호출 단위: 10, 보다 오래 걸리는 경우 hello 에이전트 hello 쿼리 계획을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="f0ed2-112">**예외 포착:** 코드에서 처리하는 예외에 대한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="f0ed2-113">**메서드 실행 시간:** 것 hello에 대 한 데이터는 tooexecute 특정 메서드를 제공 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="f0ed2-114">toouse hello Java 에이전트에 설치한 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="f0ed2-115">웹 앱으로 hello로 계측 해야 [Application Insights Java SDK][java]합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="f0ed2-116">Java 용 Application Insights 에이전트 hello 설치</span><span class="sxs-lookup"><span data-stu-id="f0ed2-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="f0ed2-117">Hello 컴퓨터에서 Java 서버에서 실행 [hello 에이전트 다운로드](https://aka.ms/aijavasdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="f0ed2-118">Hello 응용 프로그램 서버 시작 스크립트를 편집 하 고 다음 JVM hello 추가:</span><span class="sxs-lookup"><span data-stu-id="f0ed2-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="f0ed2-119">`javaagent:`*전체 경로 toohello 에이전트 JAR 파일*</span><span class="sxs-lookup"><span data-stu-id="f0ed2-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="f0ed2-120">예를 들어 Linux 컴퓨터의 Tomcat에서:</span><span class="sxs-lookup"><span data-stu-id="f0ed2-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="f0ed2-121">응용 프로그램 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="f0ed2-122">Hello 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="f0ed2-122">Configure hello agent</span></span>
<span data-ttu-id="f0ed2-123">라는 파일을 만들어 `AI-Agent.xml` hello에 넣는 hello 에이전트 JAR 파일과 같은 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="f0ed2-124">Hello xml 인의 hello 콘텐츠를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="f0ed2-125">다음 예제에서는 tooinclude hello를 편집 하거나 원하는 hello 기능을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

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

<span data-ttu-id="f0ed2-126">Tooenable 보고서 예외 및 개별 메서드에 대 한 메서드 타이밍 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="f0ed2-127">기본적으로 `reportExecutionTime`은 true이고 `reportCaughtExceptions`는 false입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="f0ed2-128">Hello 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="f0ed2-128">View hello data</span></span>
<span data-ttu-id="f0ed2-129">Application Insights 리소스 hello, 집계 된 원격 종속성과 메서드 실행 시간 표시 [hello 성능에서 타일][metrics]합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="f0ed2-130">종속성, 예외 및 메서드가 보고서의 개별 인스턴스에 대 한 toosearch 열고 [검색][diagnostic]합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ed2-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="f0ed2-131">[종속성 문제 진단 - 자세한 내용](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="f0ed2-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="f0ed2-132">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="f0ed2-132">Questions?</span></span> <span data-ttu-id="f0ed2-133">문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f0ed2-133">Problems?</span></span>
* <span data-ttu-id="f0ed2-134">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="f0ed2-134">No data?</span></span> [<span data-ttu-id="f0ed2-135">방화벽 예외 설정</span><span class="sxs-lookup"><span data-stu-id="f0ed2-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="f0ed2-136">Java 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f0ed2-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md

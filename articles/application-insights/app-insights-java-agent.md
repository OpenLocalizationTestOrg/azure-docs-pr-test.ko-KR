---
title: "Azure Application Insights에서 Java 웹앱에 대한 성능 모니터링 | Microsoft Docs"
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="3155e-103">종속성, 예외 및 Java 웹앱에서의 실행 시간을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="3155e-104">[Application Insights로 Java 웹앱을 계측][java]한 경우, Java Agent를 사용하여 코드의 변경 없이 보다 심층적인 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="3155e-105">**종속성:** 응용 프로그램이 다음을 포함한 다른 구성 요소에 수행하는 호출에 대한 데이터:</span><span class="sxs-lookup"><span data-stu-id="3155e-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="3155e-106">**REST 호출** .</span><span class="sxs-lookup"><span data-stu-id="3155e-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="3155e-107">**Redis** 호출.</span><span class="sxs-lookup"><span data-stu-id="3155e-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="3155e-108">호출 시간이 10초보다 길면, 에이전트도 호출 인수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="3155e-109">**[JDBC 호출](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB 또는 Apache Derby DB</span><span class="sxs-lookup"><span data-stu-id="3155e-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="3155e-110">"executeBatch"호출이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="3155e-111">MySQL 및 PostgreSQL의 경우 호출 시간이 10초보다 길면 에이전트가 쿼리 계획을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="3155e-112">**예외 포착:** 코드에서 처리하는 예외에 대한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="3155e-113">**메서드 실행 시간:** 특정 메서드를 실행하는 데 걸리는 시간에 대한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="3155e-114">Java 에이전트를 사용하려면 사용자의 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="3155e-115">[Application Insights Java SDK][java]를 사용하여 웹앱을 계측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="3155e-116">Java용 Application Insights 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="3155e-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="3155e-117">Java 서버를 실행 중인 컴퓨터에서 [에이전트를 다운로드](https://aka.ms/aijavasdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="3155e-118">응용 프로그램 서버 시작 스크립트를 편집하여 다음 JVM을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="3155e-119">`javaagent:`*에이전트 JAR 파일에 대한 전체 경로*</span><span class="sxs-lookup"><span data-stu-id="3155e-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="3155e-120">예를 들어 Linux 컴퓨터의 Tomcat에서:</span><span class="sxs-lookup"><span data-stu-id="3155e-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="3155e-121">응용 프로그램 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="3155e-122">에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="3155e-122">Configure the agent</span></span>
<span data-ttu-id="3155e-123">`AI-Agent.xml` 파일을 만들어 에이전트 JAR 파일과 동일한 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="3155e-124">xml 파일의 내용을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-124">Set the content of the xml file.</span></span> <span data-ttu-id="3155e-125">다음 예제를 편집하여 원하는 기능을 포함 또는 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="3155e-126">개별 메서드에 대한 메서드 타이밍과 예외를 보고할 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="3155e-127">기본적으로 `reportExecutionTime`은 true이고 `reportCaughtExceptions`는 false입니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="3155e-128">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="3155e-128">View the data</span></span>
<span data-ttu-id="3155e-129">Application Insights 리소스에서 원격 종속성과 메서드 실행 시간의 합계는 [성능 타일 아래][metrics]에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="3155e-130">종속성의 개별 인스턴스, 예외 및 메서드 보고서를 찾으려면 [검색][diagnostic]을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3155e-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="3155e-131">[종속성 문제 진단 - 자세한 내용](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="3155e-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="3155e-132">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="3155e-132">Questions?</span></span> <span data-ttu-id="3155e-133">문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="3155e-133">Problems?</span></span>
* <span data-ttu-id="3155e-134">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="3155e-134">No data?</span></span> [<span data-ttu-id="3155e-135">방화벽 예외 설정</span><span class="sxs-lookup"><span data-stu-id="3155e-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="3155e-136">Java 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3155e-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md

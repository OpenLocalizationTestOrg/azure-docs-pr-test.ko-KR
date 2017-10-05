---
title: "Azure Application Insights에서 Java 추적 로그 탐색 | Microsoft Docs"
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
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="2e5b5-103">Application Insights에서 Java 추적 로그 탐색</span><span class="sxs-lookup"><span data-stu-id="2e5b5-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="2e5b5-104">추적에 Logback 또는 Log4J(v1.2 또는 v2.0)를 사용하는 경우 추적 로그를 탐색 및 검색할 수 있는 Application Insights에 추적 로그를 자동으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="2e5b5-105">Java SDK 설치</span><span class="sxs-lookup"><span data-stu-id="2e5b5-105">Install the Java SDK</span></span>

<span data-ttu-id="2e5b5-106">아직 수행하지 않은 경우 [Java용 Application Insights SDK][java]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="2e5b5-107">HTTP 요청을 추적하지 않으려는 경우 .xml 구성 파일의 대부분을 생략할 수 있지만 적어도 `InstrumentationKey` 요소는 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="2e5b5-108">SDK를 초기화하려면 `new TelemetryClient()`도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="2e5b5-109">프로젝트에 로깅 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="2e5b5-109">Add logging libraries to your project</span></span>
<span data-ttu-id="2e5b5-110">*프로젝트에 적합한 방법을 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="2e5b5-111">Maven을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="2e5b5-111">If you're using Maven...</span></span>
<span data-ttu-id="2e5b5-112">빌드에 Maven을 사용하도록 프로젝트가 이미 설정된 경우 pom.xml 파일에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="2e5b5-113">그런 다음 프로젝트 종속성을 새로 고쳐 다운로드한 이진을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="2e5b5-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="2e5b5-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="2e5b5-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="2e5b5-117">Gradle을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="2e5b5-117">If you're using Gradle...</span></span>
<span data-ttu-id="2e5b5-118">빌드에 Gradle을 사용하도록 프로젝트가 이미 설정된 경우 다음 줄 중 하나를 build.gradle 파일의 `dependencies` 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="2e5b5-119">그런 다음 프로젝트 종속성을 새로 고쳐 다운로드한 이진을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="2e5b5-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="2e5b5-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="2e5b5-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="2e5b5-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="2e5b5-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="2e5b5-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="2e5b5-123">기타...</span><span class="sxs-lookup"><span data-stu-id="2e5b5-123">Otherwise ...</span></span>
<span data-ttu-id="2e5b5-124">적합한 어펜더를 다운로드 및 추출한 다음 적합한 라이브러리를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="2e5b5-125">로거</span><span class="sxs-lookup"><span data-stu-id="2e5b5-125">Logger</span></span> | <span data-ttu-id="2e5b5-126">다운로드</span><span class="sxs-lookup"><span data-stu-id="2e5b5-126">Download</span></span> | <span data-ttu-id="2e5b5-127">라이브러리</span><span class="sxs-lookup"><span data-stu-id="2e5b5-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e5b5-128">Logback</span><span class="sxs-lookup"><span data-stu-id="2e5b5-128">Logback</span></span> |[<span data-ttu-id="2e5b5-129">Logback 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="2e5b5-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="2e5b5-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="2e5b5-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="2e5b5-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="2e5b5-131">Log4J v2.0</span></span> |[<span data-ttu-id="2e5b5-132">Log4J v2 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="2e5b5-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="2e5b5-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="2e5b5-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="2e5b5-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="2e5b5-134">Log4j v1.2</span></span> |[<span data-ttu-id="2e5b5-135">Log4J v1.2 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="2e5b5-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="2e5b5-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="2e5b5-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="2e5b5-137">로깅 프레임워크에 어펜더 추가</span><span class="sxs-lookup"><span data-stu-id="2e5b5-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="2e5b5-138">추적 가져오기를 시작하려면 관련 코드 조각을 Log4J 및 Logback 구성 파일과 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="2e5b5-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="2e5b5-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="2e5b5-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="2e5b5-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="2e5b5-142">Application Insights 어펜더는 루트 로거만이 아니라 구성된 모든 로거에 의해 참조될 수 있습니다(위의 코드 샘플에 표시).</span><span class="sxs-lookup"><span data-stu-id="2e5b5-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="2e5b5-143">Application Insights 포털에서 추적 탐색</span><span class="sxs-lookup"><span data-stu-id="2e5b5-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="2e5b5-144">이제 Application Insights에 추적을 전송하도록 프로젝트를 구성했으며 [검색][diagnostic] 블레이드의 Application Insights 포털에서 이러한 추적을 보고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e5b5-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![Application Insights 포털에서 검색을 엽니다.](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="2e5b5-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e5b5-146">Next steps</span></span>
<span data-ttu-id="2e5b5-147">[진단 검색][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="2e5b5-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md



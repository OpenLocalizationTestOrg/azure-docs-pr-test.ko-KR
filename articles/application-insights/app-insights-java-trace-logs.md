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
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="a3f48-103">Application Insights에서 Java 추적 로그 탐색</span><span class="sxs-lookup"><span data-stu-id="a3f48-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="a3f48-104">Log4J 또는 Logback을 사용 중인 경우 (v 1.2 또는 v2.0) 추적을 위한 tooApplication Insights 탐색 하 고 검색 하 수를 자동으로 전송 하 여 추적 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="a3f48-105">Hello Java SDK 설치</span><span class="sxs-lookup"><span data-stu-id="a3f48-105">Install hello Java SDK</span></span>

<span data-ttu-id="a3f48-106">아직 수행하지 않은 경우 [Java용 Application Insights SDK][java]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="a3f48-107">(대부분의 hello.xml 구성 파일을 생략할 수 있습니다 하지만 hello 이상 포함 해야, tootrack HTTP 요청 하지 않으려는 경우 `InstrumentationKey` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="a3f48-108">또한를 호출 해야 `new TelemetryClient()` tooinitialize hello SDK.)</span><span class="sxs-lookup"><span data-stu-id="a3f48-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="a3f48-109">로깅 라이브러리 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="a3f48-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="a3f48-110">*프로젝트에 대 한 적절 한 방법으로 hello를 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a3f48-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="a3f48-111">Maven을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="a3f48-111">If you're using Maven...</span></span>
<span data-ttu-id="a3f48-112">Toouse Maven 빌드에 대 한 프로젝트에 이미 설치 되 면 hello 코드 조각을 pom.xml 파일에 다음 중 하나를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="a3f48-113">그런 다음 hello 프로젝트 종속성을 tooget hello 다운로드 된 이진 파일을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="a3f48-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="a3f48-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="a3f48-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="a3f48-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="a3f48-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="a3f48-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="a3f48-117">Gradle을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="a3f48-117">If you're using Gradle...</span></span>
<span data-ttu-id="a3f48-118">Hello 줄 toohello 다음 중 하나를 toouse Gradle 빌드에 대 한 프로젝트에 이미 설치 되 면 하는 경우 추가 `dependencies` 그룹의 build.gradle 파일이에서:</span><span class="sxs-lookup"><span data-stu-id="a3f48-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="a3f48-119">그런 다음 hello 프로젝트 종속성을 tooget hello 다운로드 된 이진 파일을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="a3f48-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="a3f48-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="a3f48-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="a3f48-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="a3f48-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="a3f48-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="a3f48-123">기타...</span><span class="sxs-lookup"><span data-stu-id="a3f48-123">Otherwise ...</span></span>
<span data-ttu-id="a3f48-124">다운로드 하 고 적절 한 hello 어 펜더를 추출 한 다음 hello 적절 한 라이브러리 tooyour 프로젝트 추가:</span><span class="sxs-lookup"><span data-stu-id="a3f48-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="a3f48-125">로거</span><span class="sxs-lookup"><span data-stu-id="a3f48-125">Logger</span></span> | <span data-ttu-id="a3f48-126">다운로드</span><span class="sxs-lookup"><span data-stu-id="a3f48-126">Download</span></span> | <span data-ttu-id="a3f48-127">라이브러리</span><span class="sxs-lookup"><span data-stu-id="a3f48-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3f48-128">Logback</span><span class="sxs-lookup"><span data-stu-id="a3f48-128">Logback</span></span> |[<span data-ttu-id="a3f48-129">Logback 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="a3f48-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="a3f48-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="a3f48-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="a3f48-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="a3f48-131">Log4J v2.0</span></span> |[<span data-ttu-id="a3f48-132">Log4J v2 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="a3f48-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="a3f48-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="a3f48-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="a3f48-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="a3f48-134">Log4j v1.2</span></span> |[<span data-ttu-id="a3f48-135">Log4J v1.2 어펜더를 사용한 SDK</span><span class="sxs-lookup"><span data-stu-id="a3f48-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="a3f48-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="a3f48-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="a3f48-137">Hello 어 펜더 tooyour 로깅 프레임 워크 추가</span><span class="sxs-lookup"><span data-stu-id="a3f48-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="a3f48-138">추적, 코드 toohello Log4J 또는 Logback 구성 파일의 병합 hello 관련 조각을 toostart:</span><span class="sxs-lookup"><span data-stu-id="a3f48-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="a3f48-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="a3f48-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="a3f48-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="a3f48-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="a3f48-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="a3f48-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="a3f48-142">hello Application Insights 어 펜더가 제공 (위의 hello 코드 샘플에 표시)으로 구성 된 모든로 거를 여는 것 뿐 아니라 hello 루트 로거에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="a3f48-143">Hello Application Insights 포털에서 사용자 추적 탐색</span><span class="sxs-lookup"><span data-stu-id="a3f48-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="a3f48-144">구성한 경우 했으므로 프로젝트 toosend tooApplication Insights 추적, 확인 및 hello에 hello Application Insights 포털에서 이러한 추적을 검색할 수 있습니다 [검색] [ diagnostic] 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a3f48-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![Hello Application Insights 포털에서 검색 시작](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="a3f48-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3f48-146">Next steps</span></span>
<span data-ttu-id="a3f48-147">[진단 검색][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="a3f48-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md



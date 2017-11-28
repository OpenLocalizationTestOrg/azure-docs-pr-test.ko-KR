---
title: "Azure Application Insights를 사용한 웹 응용 프로그램 분석 aaaJava | Microsoft Docs"
description: "Application Insights를 사용하여 Java 웹앱에 대한 응용 프로그램 성능 모니터링. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="3369b-103">Java 웹 프로젝트에서 Application Insights 시작하기</span><span class="sxs-lookup"><span data-stu-id="3369b-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="3369b-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) 때 도움이 되는 웹 개발자 hello 성능 및 라이브 응용 프로그램의 사용을 이해 하는 확장 가능한 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="3369b-105">가 사용할[검색 및 진단 성능 문제 및 예외](app-insights-detect-triage-diagnose.md), 및 [코드를 작성] [ api] 사용자가 앱을 사용 하 여 수행할 tootrack 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![샘플 데이터](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="3369b-107">Application Insights는 Linux, Unix 또는 Windows에서 실행되는 Java 앱을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="3369b-108">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-108">You need:</span></span>

* <span data-ttu-id="3369b-109">Oracle JRE 1.6 이상 또는 Zulu JRE 1.6 이상</span><span class="sxs-lookup"><span data-stu-id="3369b-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="3369b-110">구독 너무[Microsoft Azure](https://azure.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="3369b-111">*너무 hello 대체 절차를 이미 라이브 상태인 웹 앱이 있는 경우 수행할 수 있습니다[hello SDK hello 웹 서버에서 런타임에 추가](app-insights-java-live.md)합니다. 그 대신 hello 코드를 다시 작성을 방지 하지만 hello 옵션 toowrite 코드 tootrack 사용자 활동을 활용할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="3369b-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="3369b-112">1. Application Insights 계측 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="3369b-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="3369b-113">Toohello 로그인 [Microsoft Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3369b-114">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="3369b-114">Create an Application Insights resource.</span></span> <span data-ttu-id="3369b-115">Hello 응용 프로그램 종류 tooJava 웹 응용 프로그램을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-115">Set hello application type tooJava web application.</span></span>

    ![이름을 채우고 Java 웹 앱을 선택하여 만들기 클릭](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="3369b-117">Hello 새 리소스의 계측 키를 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="3369b-118">해야 toopaste이이 키를 코드 프로젝트에 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="3369b-120">2. Java tooyour 프로젝트에 대 한 hello Application Insights SDK 추가</span><span class="sxs-lookup"><span data-stu-id="3369b-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="3369b-121">*프로젝트에 대 한 적절 한 방법으로 hello를 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="3369b-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="3369b-122">사용 중인 경우 toocreate Maven 또는 동적 웹 프로젝트를 Eclipse 중...</span><span class="sxs-lookup"><span data-stu-id="3369b-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="3369b-123">사용 하 여 hello [플러그 인 Java 용 Application Insights SDK][eclipse]합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="3369b-124">Maven을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="3369b-124">If you're using Maven...</span></span>
<span data-ttu-id="3369b-125">Toouse Maven 빌드에 대 한 프로젝트에 이미 설치 되 면 하는 경우 다음 코드 tooyour pom.xml 파일 hello를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="3369b-126">그런 다음 새로 고침 hello 프로젝트 종속성 tooget hello 이진 파일 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="3369b-127">*빌드 또는 체크섬 유효성 검사 오류가 있나요?*</span><span class="sxs-lookup"><span data-stu-id="3369b-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="3369b-128">`<version>1.0.n</version>`과(와) 같은 특정 버전을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="3369b-129">Hello에 hello 최신 버전을 찾을 수 있습니다 [SDK 릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) 또는 우리의 [Maven 아티팩트](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="3369b-130">*Tooupdate tooa 필요한 새 SDK?*</span><span class="sxs-lookup"><span data-stu-id="3369b-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="3369b-131">프로젝트의 종속성을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="3369b-132">Gradle을 사용하는 경우...</span><span class="sxs-lookup"><span data-stu-id="3369b-132">If you're using Gradle...</span></span>
<span data-ttu-id="3369b-133">Toouse Gradle 빌드에 대 한 프로젝트에 이미 설치 되 면 병합 hello 다음 코드 tooyour의 build.gradle 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="3369b-134">새로 고침 hello 프로젝트 종속성 tooget hello 이진 파일의 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="3369b-135">*빌드 또는 체크섬 유효성 검사 오류가 있나요? 다음과 같은 특정 버전을 사용해 봅니다*`version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="3369b-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="3369b-136">*Hello에 hello 최신 버전을 찾을 수 있습니다 [SDK 릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)합니다.*</span><span class="sxs-lookup"><span data-stu-id="3369b-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="3369b-137">*tooupdate tooa 새 SDK*</span><span class="sxs-lookup"><span data-stu-id="3369b-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="3369b-138">프로젝트의 종속성을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="3369b-139">기타...</span><span class="sxs-lookup"><span data-stu-id="3369b-139">Otherwise ...</span></span>
<span data-ttu-id="3369b-140">수동으로 hello SDK를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="3369b-141">Hello 다운로드 [Java 용 Application Insights SDK](https://aka.ms/aijavasdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="3369b-142">Hello 바이너리 hello zip 파일에서 추출한 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="3369b-143">질문...</span><span class="sxs-lookup"><span data-stu-id="3369b-143">Questions...</span></span>
* <span data-ttu-id="3369b-144">*Hello 관계 hello 이란 `-core` 및 `-web` hello zip의 구성 요소?*</span><span class="sxs-lookup"><span data-stu-id="3369b-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="3369b-145">`applicationinsights-core`운영 체제 미 설치 API hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="3369b-146">이 구성 요소는 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-146">You always need this component.</span></span>
  * <span data-ttu-id="3369b-147">`applicationinsights-web` 은 HTTP 요청 수와 응답 시간을 추적하는 메트릭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="3369b-148">사용자가 원격 분석 자동 수집을 원하지 않는 경우 이 구성 요소를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="3369b-149">예를 들어 원하는 toowrite 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="3369b-150">*tooupdate hello SDK 변경 내용을 게시 하는 경우*</span><span class="sxs-lookup"><span data-stu-id="3369b-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="3369b-151">Hello를 최신 버전 다운로드 [Java 용 Application Insights SDK](https://aka.ms/qqkaq6) 예전 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="3369b-152">변경 내용을 hello에 설명 된 [SDK 릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="3369b-153">3. Application Insights .xml 파일 추가</span><span class="sxs-lookup"><span data-stu-id="3369b-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="3369b-154">프로젝트에서 ApplicationInsights.xml toohello 리소스 폴더를 추가 하거나 tooyour 프로젝트의 배포 클래스 경로 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="3369b-155">Hello에 다음과 같은 XML을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="3369b-156">Hello Azure 포털에서에서 가져온 hello 계측 키를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="3369b-157">hello 계측 키 원격 분석의 모든 항목이 함께 전송 되 고 Application Insights toodisplay 지시, 리소스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="3369b-158">hello HTTP 요청 구성 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="3369b-159">자동으로 요청 및 응답 시간 toohello 포털에 대 한 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="3369b-160">상관 관계 이벤트는 또한 toohello HTTP 요청 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="3369b-161">Hello 서버에서 수신 하는 식별자 tooeach 요청이 할당 hello 속성 'Operation.Id'로 원격 분석의 속성 tooevery 항목으로이 식별자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="3369b-162">Toocorrelate hello 원격 분석에서 필터를 설정 하 여 연결 된 각 요청 허용 [진단 검색][diagnostic]합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="3369b-163">hello Application Insights 키로 전달할 수 동적으로 hello에서 Azure 포털 시스템 속성 (-DAPPLICATION_INSIGHTS_IKEY your_ikey =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="3369b-164">정의된 속성이 없는 경우 Azure 앱 설정에서 환경 변수(APPLICATION_INSIGHTS_IKEY)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="3369b-165">두 hello 속성이 정의 되지 않습니다 hello 기본 InstrumentationKey ApplicationInsights.xml에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="3369b-166">이 시퀀스를 사용 하면 toomanage 다양 한 환경에 대 한 다른 InstrumentationKeys 동적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="3369b-167">다른 방법 tooset hello 계측 키</span><span class="sxs-lookup"><span data-stu-id="3369b-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="3369b-168">Application Insights SDK는 다음 순서로 hello 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="3369b-169">시스템 속성: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="3369b-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="3369b-170">환경 변수: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="3369b-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="3369b-171">구성 파일: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="3369b-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="3369b-172">또한 [코드로 설정](app-insights-api-custom-events-metrics.md#ikey)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="3369b-173">4. HTTP 필터 추가</span><span class="sxs-lookup"><span data-stu-id="3369b-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="3369b-174">hello 마지막 구성 단계 hello HTTP 요청 구성 요소 toolog 각 웹 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="3369b-175">(필요 없음 hello 완전 API 려는 경우.)</span><span class="sxs-lookup"><span data-stu-id="3369b-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="3369b-176">찾아 프로젝트 및 응용 프로그램 필터 구성 된 hello 웹 응용 프로그램 노드 아래 코드를 다음 병합 hello에 hello web.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="3369b-177">다른 모든 필터 전에 tooget hello 가장 정확한 결과 hello 필터 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="3369b-178">Spring Web MVC 3.1 이상을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="3369b-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="3369b-179">이러한 요소를 편집 *-servlet.xml tooinclude hello Application Insights 패키지:</span><span class="sxs-lookup"><span data-stu-id="3369b-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="3369b-180">Struts 2를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="3369b-180">If you're using Struts 2</span></span>
<span data-ttu-id="3369b-181">이 항목 toohello Struts 구성 파일 (일반적으로 명명 된 struts.xml 또는 struts default.xml)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="3369b-182">(기본 스택에 정의 된 인터셉터를 사용 하도록 설정한 경우 hello 인터셉터 간단히 추가할 수 있습니다 toothat 스택.)</span><span class="sxs-lookup"><span data-stu-id="3369b-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="3369b-183">5. 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3369b-183">5. Run your application</span></span>
<span data-ttu-id="3369b-184">개발 컴퓨터에서 디버그 모드에서 실행 하거나 tooyour 서버를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="3369b-185">6. Application Insights에서 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="3369b-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="3369b-186">tooyour Application Insights 리소스 반환 [Microsoft Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3369b-187">HTTP 요청 데이터 hello 개요 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="3369b-188">(없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="3369b-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![샘플 데이터](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="3369b-190">[메트릭에 대해 자세히 알아봅니다.][metrics]</span><span class="sxs-lookup"><span data-stu-id="3369b-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="3369b-191">클릭 광고 더 자세한 모든 차트 toosee 메트릭을 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="3369b-192">Application Insights hello MVC 응용 프로그램에 대 한 HTTP 요청 형식이 가정: `VERB controller/action`합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="3369b-193">예를들어, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` 및 `GET Home/Product/sdf96vws`은(는) `GET Home/Product`(으)로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="3369b-194">이 그룹화를 통해 요청 수와 같은 의미 있는 집계 및 요청에 대한 평균 실행 시간을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="3369b-195">인스턴스 데이터</span><span class="sxs-lookup"><span data-stu-id="3369b-195">Instance data</span></span>
<span data-ttu-id="3369b-196">특정 요청 형식 toosee 개별 인스턴스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="3369b-197">집계된 데이터, 평균, 개수, 합계로 저장 및 표시된 인스턴스 데이터와 HTTP 요청, 예외, 페이지 보기 또는 사용자 지정 이벤트의 개별 보고서 등 두 종류의 데이터가 Application Insights에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="3369b-198">요청의 hello 속성을 볼 때에 요청 및 예외와 같은 연관 된 hello 원격 분석 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="3369b-199">분석: 강력한 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="3369b-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="3369b-200">더 많은 데이터를 누적 두 tooaggregate 데이터와 toofind 개별 인스턴스 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="3369b-201">[분석](app-insights-analytics.md) 은 성능 및 사용 이해 및 진단 목적 모두에 강력한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![분석 예제](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="3369b-203">7. Hello 서버에서 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-203">7. Install your app on hello server</span></span>
<span data-ttu-id="3369b-204">이제 앱 toohello 서버를 게시, 사용자가을 사용 하 고 hello 포털에 표시 하는 hello 원격 분석을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="3369b-205">방화벽이 허용 응용 프로그램 toosend 원격 분석 toothese 포트 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="3369b-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="3369b-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="3369b-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="3369b-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="3369b-208">나가는 트래픽이 방화벽을 통해 라우팅되어야 하는 경우 시스템 속성 `http.proxyHost` 및 `http.proxyPort`를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="3369b-209">Windows 서버에 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="3369b-210">Microsoft Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="3369b-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="3369b-211">(이 구성 요소를 통해 성능 카운터를 사용할 수 있게 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3369b-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="3369b-212">예외 및 요청 실패</span><span class="sxs-lookup"><span data-stu-id="3369b-212">Exceptions and request failures</span></span>
<span data-ttu-id="3369b-213">처리되지 않은 예외는 자동으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-213">Unhandled exceptions are automatically collected:</span></span>

![설정 열기, 오류](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="3369b-215">다른 예외에서 toocollect 데이터를 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="3369b-216">[코드에서 tootrackException()를 호출 하는 insert][apiexceptions]합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="3369b-217">[서버에 hello Java 에이전트 설치](app-insights-java-agent.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="3369b-218">Toowatch hello 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="3369b-219">메서드 호출 및 외부 종속성 모니터링</span><span class="sxs-lookup"><span data-stu-id="3369b-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="3369b-220">[Hello Java 에이전트 설치](app-insights-java-agent.md) toolog 지정 내부 메서드 및 타이밍 데이터와 함께 JDBC를 통해 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="3369b-221">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="3369b-221">Performance counters</span></span>
<span data-ttu-id="3369b-222">열기 **설정**, **서버**, toosee 성능 카운터의 범위.</span><span class="sxs-lookup"><span data-stu-id="3369b-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="3369b-223">성능 카운터 수집 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3369b-223">Customize performance counter collection</span></span>
<span data-ttu-id="3369b-224">hello 표준 성능 카운터 집합의 toodisable 컬렉션 hello 코드 hello ApplicationInsights.xml 파일의 hello 루트 노드 아래에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="3369b-225">추가 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="3369b-225">Collect additional performance counters</span></span>
<span data-ttu-id="3369b-226">추가 성능 카운터 toobe 수집된을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="3369b-227">JMX 카운터 (hello Java 가상 컴퓨터에 의해 노출 됨)</span><span class="sxs-lookup"><span data-stu-id="3369b-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="3369b-228">`displayName`– hello Application Insights 포털에 표시 된 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="3369b-229">`objectName`– hello JMX 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="3369b-230">`attribute`– hello JMX 개체 이름 toofetch hello 특성</span><span class="sxs-lookup"><span data-stu-id="3369b-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="3369b-231">`type`(선택 사항)-JMX 개체의 특성 유형의 hello:</span><span class="sxs-lookup"><span data-stu-id="3369b-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="3369b-232">기본값: int 또는 long과 같은 단순 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="3369b-233">`composite`: hello 성능 카운터 데이터는 'Attribute.Data' hello 형식으로 되어</span><span class="sxs-lookup"><span data-stu-id="3369b-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="3369b-234">`tabular`: hello 성능 카운터 데이터는 테이블 행의 hello 형식</span><span class="sxs-lookup"><span data-stu-id="3369b-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="3369b-235">Windows 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="3369b-235">Windows performance counters</span></span>
<span data-ttu-id="3369b-236">각 [Windows 성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 범주의 멤버인 (hello에서 필드는 클래스의 멤버가 동일한 방식으로).</span><span class="sxs-lookup"><span data-stu-id="3369b-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="3369b-237">범주는 전역일 수 있으며, 번호 또는 이름이 지정된 인스턴스를 가질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="3369b-238">displayName hello Application Insights 포털에 표시 된 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="3369b-239">categoryName hello 성능 카운터 범주 (성능 개체)이 성능 카운터와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="3369b-240">counterName hello 성능 카운터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="3369b-241">-instanceName hello hello 성능 카운터 범주 인스턴스 이름, 또는 빈 문자열 ("") hello 범주에는 단일 인스턴스가 포함 된 경우.</span><span class="sxs-lookup"><span data-stu-id="3369b-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="3369b-242">Hello categoryName 프로세스, and toocollect 원하는 성능 카운터를 hello hello 현재 JVM 프로세스에서 실행 중인 앱을 지정 `"__SELF__"`합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="3369b-243">성능 카운터에서가 [메트릭 탐색기][metrics]에서 사용자 지정 메트릭으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="3369b-244">Unix 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="3369b-244">Unix performance counters</span></span>
* <span data-ttu-id="3369b-245">[Collectd hello Application Insights 플러그 인 설치](app-insights-java-collectd.md) tooget 다양 한 시스템 및 네트워크 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="3369b-246">사용자 및 세션 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="3369b-246">Get user and session data</span></span>
<span data-ttu-id="3369b-247">이제 웹 서버에서 원격 분석을 보내려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="3369b-248">이제 tooget 모니터링 더 추가할 수 있습니다 hello 응용 프로그램의 전체 360도 보기:</span><span class="sxs-lookup"><span data-stu-id="3369b-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="3369b-249">[원격 분석 tooyour 웹 페이지 추가] [ usage] 뷰와 사용자 메트릭을 toomonitor 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="3369b-250">[웹 테스트 설정] [ availability] toomake 라이브 및 응답성이 뛰어난 응용 프로그램 없이 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="3369b-251">로그 추적 캡처</span><span class="sxs-lookup"><span data-stu-id="3369b-251">Capture log traces</span></span>
<span data-ttu-id="3369b-252">Application Insights tooslice를 사용 하 여 수 있으며 Log4J 또는 Logback을 다른 로깅 프레임 워크에서 로그를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="3369b-253">HTTP 요청 및 기타 원격 분석 hello 로그에 상관 관계를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="3369b-254">[방법을 알아봅니다][javalogs].</span><span class="sxs-lookup"><span data-stu-id="3369b-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="3369b-255">사용자 고유의 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="3369b-255">Send your own telemetry</span></span>
<span data-ttu-id="3369b-256">Hello SDK를 설치한 다음 했으므로 직접 원격 분석 API toosend hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="3369b-257">[사용자 지정 이벤트 및 메트릭을 추적] [ api] toolearn 응용 프로그램과 함께 수행 하는 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="3369b-258">[이벤트 및 로그를 검색할] [ diagnostic] toohelp 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="3369b-259">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="3369b-259">Availability web tests</span></span>
<span data-ttu-id="3369b-260">Application Insights는 사용자가 정기적으로 toocheck 및 잘 응답에서 웹 사이트를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="3369b-261">[tooset][availability]를 웹 테스트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-261">[tooset up][availability], click Web tests.</span></span>

![웹 테스트 클릭한 다음 웹 테스트 추가](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="3369b-263">사이트가 다운되는 경우 응답 시간 차트는 물론 이메일 알림을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![웹 테스트의 예](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="3369b-265">[가용성 웹 테스트에 대한 자세히 알아봅니다.][availability]</span><span class="sxs-lookup"><span data-stu-id="3369b-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="3369b-266">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="3369b-266">Questions?</span></span> <span data-ttu-id="3369b-267">문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="3369b-267">Problems?</span></span>
[<span data-ttu-id="3369b-268">Java 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3369b-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="3369b-269">비디오</span><span class="sxs-lookup"><span data-stu-id="3369b-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="3369b-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3369b-270">Next steps</span></span>
* [<span data-ttu-id="3369b-271">종속성 호출 모니터링</span><span class="sxs-lookup"><span data-stu-id="3369b-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="3369b-272">Unix 성능 카운터 모니터링</span><span class="sxs-lookup"><span data-stu-id="3369b-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="3369b-273">추가 [tooyour 웹 페이지를 모니터링](app-insights-javascript.md) toomonitor 페이지 로드 시간 면 AJAX 호출 브라우저 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="3369b-274">쓰기 [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md) hello 브라우저에서 또는 hello 서버에 tootrack 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="3369b-275">만들 [대시보드](app-insights-dashboards.md) toobring 함께 hello 시스템을 모니터링 하기 위한 주요 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="3369b-276">앱의 원격 분석을 통해 강력한 쿼리를 수행하려면 [분석](app-insights-analytics.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3369b-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="3369b-277">자세한 내용은 [Java 개발자용 Azure](/java/azure)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3369b-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md

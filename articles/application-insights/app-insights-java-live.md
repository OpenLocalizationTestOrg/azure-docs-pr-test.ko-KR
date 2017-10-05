---
title: "이미 라이브 상태인 Java 웹앱용 Application Insights"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="4648f-103">이미 라이브 상태인 Java 웹앱용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="4648f-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="4648f-104">J2EE 서버에서 이미 실행 중인 웹 응용 프로그램이 있는 경우 코드를 변경하거나 프로젝트를 다시 컴파일할 필요 없이 [Application Insights](app-insights-overview.md) 를 사용하여 모니터링을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="4648f-105">이 옵션을 사용하면 서버로 전송된 HTTP 요청, 처리되지 않은 예외 및 성능 카운터에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="4648f-106">[Microsoft Azure](https://azure.com)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="4648f-107">이 페이지의 절차는 런타임에서 웹앱에 SDK를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="4648f-108">이 런타임 계측은 소스 코드를 업데이트하거나 다시 작성하지 않을 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="4648f-109">하지만 가능하면 [소스 코드에 SDK를 추가](app-insights-java-get-started.md) 할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="4648f-110">그러면 사용자 활동을 추적하는 코드를 작성하는 등 추가 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="4648f-111">1. Application Insights 계측 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="4648f-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="4648f-112">[Microsoft Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4648f-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="4648f-113">새 Application Insights 리소스를 만들고 Java 웹 응용 프로그램에 대한 응용 프로그램 종류를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![이름을 채우고 Java 웹 앱을 선택하여 만들기 클릭](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="4648f-115">리소스가 몇 초 후에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="4648f-116">새 리소스를 열고 계측 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="4648f-117">코드 프로젝트에 이 키를 곧바로 붙여넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![새 리소스 개요에서 속성을 클릭하고 계측 키 복사](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="4648f-119">2. SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="4648f-119">2. Download the SDK</span></span>
1. <span data-ttu-id="4648f-120">[Java용 Application Insights SDK](https://aka.ms/aijavasdk)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="4648f-121">서버에서 프로젝트 이진 파일이 로드된 원본 디렉터리로 SDK 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="4648f-122">Tomcat을 사용하는 경우 이 디렉터리는 일반적으로 `webapps/<your_app_name>/WEB-INF/lib`에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="4648f-123">각 서버 인스턴스와 각 앱에 대해 이를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="4648f-124">3. Application Insights xml 파일 추가</span><span class="sxs-lookup"><span data-stu-id="4648f-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="4648f-125">SDK를 추가한 폴더에 ApplicationInsights.xml을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="4648f-126">다음 XML을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-126">Put into it the following XML.</span></span>

<span data-ttu-id="4648f-127">Azure 포털에서 가져온 계측 키를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="4648f-128">계측 키는 원격 분석의 모든 항목과 함께 전송되며 리소스에서 표시하도록 Application Insights에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="4648f-129">HTTP 요청 구성 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="4648f-130">자동으로 포털에 요청 및 응답 시간에 대한 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="4648f-131">이벤트 상관 관계는 HTTP 요청 구성 요소에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="4648f-132">이는 서버가 수신하는 요청마다 식별자를 할당하며 'Operation.Id' 속성으로 원격 분석의 모든 항목에 이 식별자를 속성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="4648f-133">[진단 검색](app-insights-diagnostic-search.md)에서 필터를 설정하여 각 요청과 연결된 원격 분석의 상관 관계를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="4648f-134">4. HTTP 필터 추가</span><span class="sxs-lookup"><span data-stu-id="4648f-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="4648f-135">프로젝트에서 web.xml 파일을 찾아 열고, 응용 프로그램 필터가 구성된 웹 앱 노드 아래 다음 코드 조각을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="4648f-136">가장 정확한 결과를 얻으려면 필터를 다른 모든 필터 전에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="4648f-137">5. 방화벽 예외를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="4648f-138">[예외를 설정하여 나가는 데이터를 내보내야](app-insights-ip-addresses.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="4648f-139">6. 웹앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="4648f-140">7. Application Insights에서 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="4648f-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="4648f-141">[Microsoft Azure 포털](https://portal.azure.com)의 Application Insights 리소스로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4648f-142">HTTP 요청에 대한 원격 분석은 개요 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="4648f-143">(없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="4648f-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![샘플 데이터](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="4648f-145">차트를 클릭하면 더 자세한 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="4648f-146">또한 요청 속성 검토 시 요청 및 예외 사항과 관련된 원격 분석 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="4648f-147">메트릭에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="4648f-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4648f-148">Next steps</span></span>
* <span data-ttu-id="4648f-149">[웹 페이지에 원격 분석을 추가](app-insights-javascript.md) 하여 페이지 보기 및 사용자 메트릭을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="4648f-150">[웹 테스트를 설정](app-insights-monitor-web-app-availability.md) 하여 응용 프로그램이 라이브 상태로 유지되며 응답하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="4648f-151">로그 추적 캡처</span><span class="sxs-lookup"><span data-stu-id="4648f-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="4648f-152">[이벤트 및 로그를 검색](app-insights-diagnostic-search.md) 하여 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4648f-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>


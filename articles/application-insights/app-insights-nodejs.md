---
title: "Azure Application Insights를 사용하여 Node.js 서비스 모니터링 | Microsoft Docs"
description: "Application Insights를 사용하여 Node.js 서비스의 성능을 모니터링하고 문제를 진단합니다."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="bfc56-103">Application Insights를 사용하여 Node.js 서비스 및 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="bfc56-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="bfc56-104">백 엔드 서비스 및 구성 요소를 배포한 후 [Azure Application Insights](app-insights-overview.md)로 모니터링하여 [성능 및 기타 문제를 신속하게 발견하고 진단](app-insights-detect-triage-diagnose.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="bfc56-105">데이터 센터, Azure VM, Web Apps, 기타 공용 클라우드 등 어느 위치에 호스트된 Node.js 서비스에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="bfc56-106">모니터링 데이터를 수신, 저장 및 탐색하려면 다음 지침에 따라 코드에 에이전트를 포함하고 Azure에서 해당 Application Insights 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="bfc56-107">에이전트는 추가 분석 및 탐색을 위해 해당 리소스로 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="bfc56-108">Node.js 에이전트는 들어오고 나가는 HTTP 요청, 여러 시스템 메트릭 및 예외를 자동으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="bfc56-109">v0.20부터는 `mongodb`, `mysql`, `redis` 등의 일반적인 타사 패키지도 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="bfc56-110">들어오는 HTTP 요청과 관련된 모든 이벤트는 좀 더 빠른 문제 해결을 위해 상호 관계가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="bfc56-111">뒷부분에서 설명할 에이전트 API를 사용하여 앱과 시스템을 수동으로 계측하면 앱과 시스템의 더 많은 요소를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![예제 성능 모니터링 차트](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="bfc56-113">시작하기</span><span class="sxs-lookup"><span data-stu-id="bfc56-113">Getting Started</span></span>

<span data-ttu-id="bfc56-114">앱 또는 서비스 모니터링을 설정하는 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="bfc56-115"><a name="resource"></a> App Insights 리소스 설정</span><span class="sxs-lookup"><span data-stu-id="bfc56-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="bfc56-116">**시작하기 전에** Azure 구독이 있는지 확인하거나 [무료 계정을 새로 만듭니다][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="bfc56-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="bfc56-117">조직에 이미 Azure 구독이 있으면 관리자가 [다음 지침][add-aad-user]에 따라 사용자를 구독에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="bfc56-118">[Azure Portal][portal]에 로그인하고 다음 그림처럼 "새로 만들기" > "개발자 도구" > "Application Insights"를 클릭하여 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="bfc56-119">리소스에는 원격 분석 데이터를 수신하기 위한 끝점, 이 데이터 저장소, 저장된 보고서 및 대시보드, 규칙 및 경고 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![App Insights 리소스 만들기](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="bfc56-121">리소스 만들기 페이지의 응용 프로그램 유형 드롭다운에서 "Node.js 응용 프로그램"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="bfc56-122">앱 유형에 따라 생성되는 기본 대시보드 및 보고서 집합이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="bfc56-123">모든 App Insights 리소스는 모든 언어 및 플랫폼에서 데이터를 수집할 수 있으므로 걱정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![새로운 App Insights 리소스 형식](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="bfc56-125"><a name="agent"></a> Node.js 에이전트 설정</span><span class="sxs-lookup"><span data-stu-id="bfc56-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="bfc56-126">이제 에이전트가 데이터를 수집할 수 있도록 앱에 에이전트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="bfc56-127">먼저 아래와 같이 리소스의 계측 키(이하 `ikey`)를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="bfc56-128">App Insights 시스템은 이 키를 사용하여 데이터를 Azure 리소스로 매핑하므로 환경 변수 또는 코드에서 에이전트가 사용할 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![계측 키 복사](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="bfc56-130">다음으로 package.json을 통해 Node.js 에이전트 라이브러리를 앱의 종속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="bfc56-131">앱의 루트 폴더에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="bfc56-132">이제 코드에서 라이브러리를 명시적으로 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="bfc56-133">에이전트는 여러 다른 라이브러리에 계측 값을 삽입합니다. 따라서 최대한 신속하게, 심지어 다른 `require` 문보다도 먼저 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="bfc56-134">시작하려면 첫 번째 .js 파일의 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="bfc56-135">`setup` 메서드는 기본적으로 모든 추적 항목에 사용할 계측 키(따라서 Azure 리소스까지)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="bfc56-136">구성 후 `start` 호출이 완료되고 원격 분석 데이터의 수집 및 송신이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="bfc56-137">ikey를 `setup()` 또는 `getClient()`에 수동으로 전달하는 대신 APPINSIGHTS\_INSTRUMENTATIONKEY 환경 변수를 통해 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="bfc56-138">이렇게 하면 ikey가 커밋된 소스 코드의 영향을 받지 않으며 다른 환경에 다른 ikey를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="bfc56-139">추가 구성 옵션은 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="bfc56-140">계측 키를 비어 있지 않은 문자열로 설정하면 원격 분석을 전송하지 않고도 에이전트를 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="bfc56-141"><a name="monitor"></a> 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="bfc56-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="bfc56-142">에이전트는 Node.js 런타임 및 일부 일반적인 타사 모듈에 대한 원격 분석 데이터를 자동으로 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="bfc56-143">이제 응용 프로그램을 사용하여 이 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="bfc56-144">그런 후 다음 그림과 같이 [Azure Portal][portal]에서 이전에 만든 Application Insights 리소스를 찾고, 개요 타임 라인에서 첫 번째 데이터 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="bfc56-145">자세한 내용을 보려면 차트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-145">Click through the charts for more details.</span></span>

![첫 번째 데이터 요소](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="bfc56-147">다음 그림과 같이 응용 프로그램 맵 단추를 클릭하여 앱에 대해 검색된 토폴로지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="bfc56-148">자세한 내용을 보려면 맵에서 구성 요소를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-148">Click through components in the map for more details.</span></span>

![간단한 앱 맵](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="bfc56-150">"조사" 섹션에 제공되는 다른 보기를 사용하여 앱에 대해 자세히 알아보고 문제를 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="bfc56-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![조사 섹션](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="bfc56-152">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="bfc56-152">No data?</span></span>

<span data-ttu-id="bfc56-153">에이전트는 제출할 데이터를 일괄 처리하기 때문에 항목이 포털에 표시될 때까지 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="bfc56-154">리소스에 데이터가 보이지 않으면 다음 해결 방법 중 일부를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bfc56-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="bfc56-155">응용 프로그램을 좀 더 사용하고 원격 분석을 생성하는 작업을 좀 더 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="bfc56-156">포털 리소스 보기에서 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="bfc56-157">차트가 주기적으로 자동 새로 고침되지만 새로 고침을 클릭하면 즉시 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="bfc56-158">[필요한 발신 포트](app-insights-ip-addresses.md)가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="bfc56-159">[검색](app-insights-diagnostic-search.md) 타일을 열고 개별 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="bfc56-160">[FAQ][]를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="bfc56-161">에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="bfc56-161">Agent Configuration</span></span>

<span data-ttu-id="bfc56-162">다음은 에이전트의 구성 메서드와 해당 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="bfc56-163">서비스에서 이벤트의 상관 관계를 완전하게 지정하려면 `.setAutoDependencyCorrelation(true)`을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="bfc56-164">이렇게 하면 에이전트가 Node.js의 비동기 콜백에서 컨텍스트를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="bfc56-165">에이전트 API</span><span class="sxs-lookup"><span data-stu-id="bfc56-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="bfc56-166">.NET 에이전트 API는 [여기](app-insights-api-custom-events-metrics.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="bfc56-167">Application Insights Node.js 클라이언트를 사용하여 모든 요청, 이벤트, 메트릭 또는 예외를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="bfc56-168">다음 예제에서는 사용 가능한 API의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfc56-168">The following example demonstrates some of the available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="bfc56-169">종속성 추적</span><span class="sxs-lookup"><span data-stu-id="bfc56-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="bfc56-170">모든 이벤트에 사용자 지정 속성 추가</span><span class="sxs-lookup"><span data-stu-id="bfc56-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="bfc56-171">HTTP GET 요청 추적</span><span class="sxs-lookup"><span data-stu-id="bfc56-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="bfc56-172">서버 시작 시간 추적</span><span class="sxs-lookup"><span data-stu-id="bfc56-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="bfc56-173">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bfc56-173">More resources</span></span>

* [<span data-ttu-id="bfc56-174">포털에서 원격 분석 모니터링</span><span class="sxs-lookup"><span data-stu-id="bfc56-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="bfc56-175">원격 분석에 분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="bfc56-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="bfc56-176">[FAQ]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="bfc56-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>

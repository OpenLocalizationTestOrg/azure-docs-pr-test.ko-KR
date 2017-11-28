---
title: "Node.js aaaMonitor Azure Application Insights를 사용 하 여 서비스 | Microsoft Docs"
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
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="b6ac9-103">Application Insights를 사용하여 Node.js 서비스 및 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="b6ac9-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="b6ac9-104">[Azure Application Insights](app-insights-overview.md) toohelp를 배포한 후 백 엔드 서비스 및 구성 요소를 모니터링 하면 [검색 하 고 성능 및 기타 문제를 신속 하 게 진단](app-insights-detect-triage-diagnose.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="b6ac9-105">데이터 센터, Azure VM, Web Apps, 기타 공용 클라우드 등 어느 위치에 호스트된 Node.js 서비스에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="b6ac9-106">tooreceive, 저장 및 모니터링 하 여 데이터 탐색, hello 지침 tooinclude 코드에서 에이전트를 다음에 따라 및 Azure에서 해당 Application Insights 리소스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="b6ac9-107">hello 에이전트 추가 분석 및 탐색에 대 한 데이터 toothat 리소스를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="b6ac9-108">hello Node.js 에이전트 들어오고 나가는 HTTP 요청, 여러 가지 시스템 메트릭 및 예외에 자동으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="b6ac9-109">v0.20부터는 `mongodb`, `mysql`, `redis` 등의 일반적인 타사 패키지도 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="b6ac9-110">빠른 문제 해결에 대 한 tooan 들어오는 HTTP 요청과 상호 관련 된 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="b6ac9-111">응용 프로그램의 더 많은 요소를 모니터링할 수 있습니다 및 수동으로 계측 하 여 시스템 뒷부분에서 설명 하는 hello 에이전트 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![예제 성능 모니터링 차트](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="b6ac9-113">시작하기</span><span class="sxs-lookup"><span data-stu-id="b6ac9-113">Getting Started</span></span>

<span data-ttu-id="b6ac9-114">앱 또는 서비스 모니터링을 설정하는 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="b6ac9-115"><a name="resource"></a> App Insights 리소스 설정</span><span class="sxs-lookup"><span data-stu-id="b6ac9-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="b6ac9-116">**시작하기 전에** Azure 구독이 있는지 확인하거나 [무료 계정을 새로 만듭니다][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="b6ac9-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="b6ac9-117">관리자가 조직에 이미 Azure 구독이 있으면 따르면 [이러한 지침] [ add-aad-user] tooadd tooit 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="b6ac9-118">이제 toohello 로그인 [Azure 포털] [ portal] hello 다음에 설명 된 대로 Application Insights 리소스 만들기-"새로 만들기"를 클릭 하 고 > "개발자 도구" > "Application Insights"입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="b6ac9-119">hello 리소스에 원격 분석 데이터 받기, 보고서 및 대시보드, 규칙 및 경고 구성 및 더 저장이 데이터에 대 한 저장소에 대 한 끝점 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![App Insights 리소스 만들기](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="b6ac9-121">Hello 리소스 만들기 페이지에서 "Node.js 응용 프로그램" hello 응용 프로그램 유형 드롭다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="b6ac9-122">hello 앱 유형을 hello 기본 집합이 대시보드 및 보고서 생성을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="b6ac9-123">모든 App Insights 리소스는 모든 언어 및 플랫폼에서 데이터를 수집할 수 있으므로 걱정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![새로운 App Insights 리소스 형식](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="b6ac9-125"><a name="agent"></a>Hello Node.js 에이전트 설정</span><span class="sxs-lookup"><span data-stu-id="b6ac9-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="b6ac9-126">이제 데이터를 수집할 수 있도록 응용 프로그램에서 시간 tooinclude hello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="b6ac9-127">리소스의 계측 키를 복사 하 여 시작 (tooas이 하 라고 프로그램 `ikey`) 아래와 같이 hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="b6ac9-128">App Insights 시스템 toospecify 필요 하므로이 키 toomap 데이터 tooyour Azure 리소스 사용 하 여 hello 환경 변수 또는 에이전트 toouse hello에 대 한 코드에서.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![계측 키 복사](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="b6ac9-130">다음으로 package.json 통해 hello Node.js 에이전트 라이브러리 tooyour 응용 프로그램의 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="b6ac9-131">응용 프로그램의 hello 루트 폴더에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="b6ac9-132">이제 tooexplicitly 부하 hello 라이브러리 코드에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="b6ac9-133">다양 한 라이브러리에 계기를 삽입 하는 hello 에이전트, 때문에 로드 해야 것도 다른 하기 전에 가능한 한 빨리 `require` 문.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="b6ac9-134">tooget 시작, 첫 번째.js 파일의 hello 위쪽에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="b6ac9-135">hello `setup` 메서드 hello 계측 키 (및 따라서 Azure 리소스) 구성 toobe 추적 된 모든 항목에 대해 기본적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="b6ac9-136">호출 `start` 구성이 완료 된 toobegin 수집 및 원격 분석 데이터를 전송 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="b6ac9-137">APPINSIGHTS hello 환경 변수를 통해 ikey 제공할 수도 있습니다\_전달 하는 대신 수동으로 너무 INSTRUMENTATIONKEY `setup()` 또는 `getClient()`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="b6ac9-138">이 연습에서는 ikeys 커밋된 소스 코드에서와 다른 환경에 대해 다른 ikeys toospecify 유지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="b6ac9-139">추가 구성 옵션은 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="b6ac9-140">Hello 계측 키 tooany 비어 있지 않은 문자열을 설정 하 여 원격 분석을 전송 하지 않고 hello 에이전트를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="b6ac9-141"><a name="monitor"></a> 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="b6ac9-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="b6ac9-142">Node.js 런타임 hello에 대 한 원격 분석 및 몇 가지 일반적인 제 3 자 모듈 hello 에이전트를 자동으로 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="b6ac9-143">응용 프로그램 지금 toogenerate를 사용 하 여이 데이터의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="b6ac9-144">그런 다음, hello [Azure 포털] [ portal] 앞에서 만든 toohello Application Insights 리소스를 찾아보고 검색할 처음 몇 가지 데이터 요소에 hello 다음 이미지와 같이 hello 개요 타임 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="b6ac9-145">자세한 내용은 hello 차트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-145">Click through hello charts for more details.</span></span>

![첫 번째 데이터 요소](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="b6ac9-147">Hello 응용 프로그램 맵 단추 tooview hello 토폴로지 hello 다음 이미지와 같이 앱에 대 한 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="b6ac9-148">자세한 내용은 hello 맵에서 구성 요소를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-148">Click through components in hello map for more details.</span></span>

![간단한 앱 맵](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="b6ac9-150">응용 프로그램에 대 한 자세한 정보 및 hello "검사" 섹션에서 사용할 수 있는 다른 보기 hello를 사용 하 여 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![조사 섹션](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="b6ac9-152">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="b6ac9-152">No data?</span></span>

<span data-ttu-id="b6ac9-153">Hello 에이전트 데이터 전송에 대 한 일괄 처리 하기 때문에 있을 수 있습니다 지연 전에 항목이 hello 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="b6ac9-154">표시 되지 않으면 데이터, 리소스에 따라 수정 하는 hello 중 일부를 시도:</span><span class="sxs-lookup"><span data-stu-id="b6ac9-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="b6ac9-155">좀 더; hello 응용 프로그램을 사용 하 여 더 많은 작업 toogenerate 더 많은 원격 분석을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="b6ac9-156">클릭 **새로 고침** hello 포털 리소스 뷰에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="b6ac9-157">차트 자동으로 새로 고쳐 자체 주기적으로 있지만이 toohappen 즉시 강제로 새로 고침.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="b6ac9-158">[필요한 발신 포트](app-insights-ip-addresses.md)가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="b6ac9-159">열기 hello [검색](app-insights-diagnostic-search.md) 바둑판식으로 배열 하 고 개별 이벤트를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="b6ac9-160">Hello 확인 [FAQ][]합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="b6ac9-161">에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="b6ac9-161">Agent Configuration</span></span>

<span data-ttu-id="b6ac9-162">다음은 hello 에이전트 구성 방법 및 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="b6ac9-163">서비스의 이벤트를 상호 연결 시키고 toofully 수 있는지 tooset `.setAutoDependencyCorrelation(true)`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="b6ac9-164">따라서 hello 에이전트 tootrack 컨텍스트 Node.js에서 비동기 콜백 간에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="b6ac9-165">에이전트 API</span><span class="sxs-lookup"><span data-stu-id="b6ac9-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="b6ac9-166">hello.NET 에이전트 API 대 한 자세한 내용은 [여기](app-insights-api-custom-events-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="b6ac9-167">요청, 이벤트, 메트릭 또는 통찰력 Node.js 응용 프로그램 클라이언트 hello를 사용 하 여 예외를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="b6ac9-168">hello 다음 예제에서는 일부 hello 사용 가능한 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-168">hello following example demonstrates some of hello available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="b6ac9-169">종속성 추적</span><span class="sxs-lookup"><span data-stu-id="b6ac9-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="b6ac9-170">사용자 지정 속성 tooall 이벤트 추가</span><span class="sxs-lookup"><span data-stu-id="b6ac9-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="b6ac9-171">HTTP GET 요청 추적</span><span class="sxs-lookup"><span data-stu-id="b6ac9-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="b6ac9-172">서버 시작 시간 추적</span><span class="sxs-lookup"><span data-stu-id="b6ac9-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="b6ac9-173">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b6ac9-173">More resources</span></span>

* [<span data-ttu-id="b6ac9-174">Hello 포털에서 원격 분석을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6ac9-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="b6ac9-175">원격 분석에 분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="b6ac9-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md

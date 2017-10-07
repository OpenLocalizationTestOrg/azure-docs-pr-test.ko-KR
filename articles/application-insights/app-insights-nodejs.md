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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Application Insights를 사용하여 Node.js 서비스 및 앱 모니터링

[Azure Application Insights](app-insights-overview.md) toohelp를 배포한 후 백 엔드 서비스 및 구성 요소를 모니터링 하면 [검색 하 고 성능 및 기타 문제를 신속 하 게 진단](app-insights-detect-triage-diagnose.md)합니다. 데이터 센터, Azure VM, Web Apps, 기타 공용 클라우드 등 어느 위치에 호스트된 Node.js 서비스에도 사용할 수 있습니다.

tooreceive, 저장 및 모니터링 하 여 데이터 탐색, hello 지침 tooinclude 코드에서 에이전트를 다음에 따라 및 Azure에서 해당 Application Insights 리소스를 설정 합니다. hello 에이전트 추가 분석 및 탐색에 대 한 데이터 toothat 리소스를 보냅니다.

hello Node.js 에이전트 들어오고 나가는 HTTP 요청, 여러 가지 시스템 메트릭 및 예외에 자동으로 모니터링할 수 있습니다. v0.20부터는 `mongodb`, `mysql`, `redis` 등의 일반적인 타사 패키지도 모니터링할 수 있습니다. 빠른 문제 해결에 대 한 tooan 들어오는 HTTP 요청과 상호 관련 된 모든 이벤트.

응용 프로그램의 더 많은 요소를 모니터링할 수 있습니다 및 수동으로 계측 하 여 시스템 뒷부분에서 설명 하는 hello 에이전트 API를 사용 합니다.

![예제 성능 모니터링 차트](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>시작하기

앱 또는 서비스 모니터링을 설정하는 단계를 살펴보겠습니다.

### <a name="resource"></a> App Insights 리소스 설정

**시작하기 전에** Azure 구독이 있는지 확인하거나 [무료 계정을 새로 만듭니다][azure-free-offer]. 관리자가 조직에 이미 Azure 구독이 있으면 따르면 [이러한 지침] [ add-aad-user] tooadd tooit 있습니다.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

이제 toohello 로그인 [Azure 포털] [ portal] hello 다음에 설명 된 대로 Application Insights 리소스 만들기-"새로 만들기"를 클릭 하 고 > "개발자 도구" > "Application Insights"입니다. hello 리소스에 원격 분석 데이터 받기, 보고서 및 대시보드, 규칙 및 경고 구성 및 더 저장이 데이터에 대 한 저장소에 대 한 끝점 포함 되어 있습니다.

![App Insights 리소스 만들기](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Hello 리소스 만들기 페이지에서 "Node.js 응용 프로그램" hello 응용 프로그램 유형 드롭다운 목록에서 선택 합니다. hello 앱 유형을 hello 기본 집합이 대시보드 및 보고서 생성을 결정 합니다. 모든 App Insights 리소스는 모든 언어 및 플랫폼에서 데이터를 수집할 수 있으므로 걱정할 필요는 없습니다.

![새로운 App Insights 리소스 형식](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Hello Node.js 에이전트 설정

이제 데이터를 수집할 수 있도록 응용 프로그램에서 시간 tooinclude hello 에이전트입니다.
리소스의 계측 키를 복사 하 여 시작 (tooas이 하 라고 프로그램 `ikey`) 아래와 같이 hello 포털에서 합니다. App Insights 시스템 toospecify 필요 하므로이 키 toomap 데이터 tooyour Azure 리소스 사용 하 여 hello 환경 변수 또는 에이전트 toouse hello에 대 한 코드에서.  

![계측 키 복사](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

다음으로 package.json 통해 hello Node.js 에이전트 라이브러리 tooyour 응용 프로그램의 종속성을 추가 합니다. 응용 프로그램의 hello 루트 폴더에서 다음을 실행 합니다.

```bash
npm install applicationinsights --save
```

이제 tooexplicitly 부하 hello 라이브러리 코드에 있어야합니다. 다양 한 라이브러리에 계기를 삽입 하는 hello 에이전트, 때문에 로드 해야 것도 다른 하기 전에 가능한 한 빨리 `require` 문. tooget 시작, 첫 번째.js 파일의 hello 위쪽에 추가 합니다.

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

hello `setup` 메서드 hello 계측 키 (및 따라서 Azure 리소스) 구성 toobe 추적 된 모든 항목에 대해 기본적으로 사용 합니다. 호출 `start` 구성이 완료 된 toobegin 수집 및 원격 분석 데이터를 전송 된 후입니다.

APPINSIGHTS hello 환경 변수를 통해 ikey 제공할 수도 있습니다\_전달 하는 대신 수동으로 너무 INSTRUMENTATIONKEY `setup()` 또는 `getClient()`합니다. 이 연습에서는 ikeys 커밋된 소스 코드에서와 다른 환경에 대해 다른 ikeys toospecify 유지 수 있습니다.

추가 구성 옵션은 아래에 설명되어 있습니다.

Hello 계측 키 tooany 비어 있지 않은 문자열을 설정 하 여 원격 분석을 전송 하지 않고 hello 에이전트를 시도할 수 있습니다.

### <a name="monitor"></a> 앱 모니터링

Node.js 런타임 hello에 대 한 원격 분석 및 몇 가지 일반적인 제 3 자 모듈 hello 에이전트를 자동으로 수집 합니다. 응용 프로그램 지금 toogenerate를 사용 하 여이 데이터의 일부입니다.

그런 다음, hello [Azure 포털] [ portal] 앞에서 만든 toohello Application Insights 리소스를 찾아보고 검색할 처음 몇 가지 데이터 요소에 hello 다음 이미지와 같이 hello 개요 타임 라인입니다. 자세한 내용은 hello 차트를 클릭 합니다.

![첫 번째 데이터 요소](./media/app-insights-nodejs/12-first-perf.png)

Hello 응용 프로그램 맵 단추 tooview hello 토폴로지 hello 다음 이미지와 같이 앱에 대 한 검색을 클릭 합니다. 자세한 내용은 hello 맵에서 구성 요소를 클릭 합니다.

![간단한 앱 맵](./media/app-insights-nodejs/06-appinsights_appmap.png)

응용 프로그램에 대 한 자세한 정보 및 hello "검사" 섹션에서 사용할 수 있는 다른 보기 hello를 사용 하 여 문제를 해결 합니다.

![조사 섹션](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>데이터가 없나요?

Hello 에이전트 데이터 전송에 대 한 일괄 처리 하기 때문에 있을 수 있습니다 지연 전에 항목이 hello 포털에 표시 됩니다. 표시 되지 않으면 데이터, 리소스에 따라 수정 하는 hello 중 일부를 시도:

* 좀 더; hello 응용 프로그램을 사용 하 여 더 많은 작업 toogenerate 더 많은 원격 분석을 수행 합니다.
* 클릭 **새로 고침** hello 포털 리소스 뷰에서 합니다. 차트 자동으로 새로 고쳐 자체 주기적으로 있지만이 toohappen 즉시 강제로 새로 고침.
* [필요한 발신 포트](app-insights-ip-addresses.md)가 열려 있는지 확인합니다.
* 열기 hello [검색](app-insights-diagnostic-search.md) 바둑판식으로 배열 하 고 개별 이벤트를 찾아보십시오.
* Hello 확인 [FAQ][]합니다.


## <a name="agent-configuration"></a>에이전트 구성

다음은 hello 에이전트 구성 방법 및 기본값입니다.

서비스의 이벤트를 상호 연결 시키고 toofully 수 있는지 tooset `.setAutoDependencyCorrelation(true)`합니다. 따라서 hello 에이전트 tootrack 컨텍스트 Node.js에서 비동기 콜백 간에 있습니다.

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

## <a name="agent-api"></a>에이전트 API

<!-- TODO: Fully document agent API. -->

hello.NET 에이전트 API 대 한 자세한 내용은 [여기](app-insights-api-custom-events-metrics.md)합니다.

요청, 이벤트, 메트릭 또는 통찰력 Node.js 응용 프로그램 클라이언트 hello를 사용 하 여 예외를 추적할 수 있습니다. hello 다음 예제에서는 일부 hello 사용 가능한 Api입니다.

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

### <a name="track-your-dependencies"></a>종속성 추적

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

### <a name="add-a-custom-property-tooall-events"></a>사용자 지정 속성 tooall 이벤트 추가

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>HTTP GET 요청 추적

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>서버 시작 시간 추적

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>추가 리소스

* [Hello 포털에서 원격 분석을 모니터링 합니다.](app-insights-dashboards.md)
* [원격 분석에 분석 쿼리 작성](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md

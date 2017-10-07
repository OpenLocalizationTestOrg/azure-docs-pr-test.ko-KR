---
title: "응용 프로그램 통찰력 FAQ aaaAzure | Microsoft Docs"
description: "Application Insights에 대한 질문과 대답입니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: 질문과 대답

## <a name="configuration-problems"></a>구성 문제
*다음을 설정하는 데 문제가 있습니다.*

* [.NET 앱](app-insights-asp-net-troubleshoot-no-data.md)
* [이미 실행 중인 앱 모니터링](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Azure 진단](app-insights-azure-diagnostics.md)
* [Java 웹앱](app-insights-java-troubleshoot.md)

*내 서버에서 데이터를 가져오지 않습니다.*

* [방화벽 예외 설정](app-insights-ip-addresses.md)
* [ASP.NET 서버 설정](app-insights-monitor-performance-live-website-now.md)
* [Java 서버 설정](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Application Insights와 같이 사용할 수 있나요...?

* [IIS 서버의 웹앱 - 온-프레미스 또는 VM](app-insights-asp-net.md)
* [Java 웹앱](app-insights-java-get-started.md)
* [Node.js 앱](app-insights-nodejs.md)
* [Azure의 Web Apps](app-insights-azure-web-apps.md)
* [Azure의 Cloud Services](app-insights-cloudservices.md)
* [Docker에서 실행되는 앱 서버](app-insights-docker.md)
* [단일 페이지 웹앱](app-insights-javascript.md)
* [SharePoint](app-insights-sharepoint.md)
* [Windows 데스크톱 앱](app-insights-windows-desktop.md)
* [기타 플랫폼](app-insights-platforms.md)

## <a name="is-it-free"></a>무료입니까?

예, 실험용입니다. Hello 기본 계획 가격 책정에서 응용 프로그램에 특정 허용 되는 데이터 매월 무료로 보낼 수 있습니다. hello 무료는 충분히 큰 toocover 개발 및 적은 수의 사용자에 대 한 앱을 게시 합니다. 처리 되지 않도록 cap tooprevent 둘 이상의 지정된 된 양의 데이터를 설정할 수 있습니다.

원격 분석의 더 큰 볼륨은 Gb hello 하 여 요금이 청구 됩니다. 방법에 대 한 몇 가지 팁 너무 제공[요금에 제한](app-insights-pricing.md)합니다.

hello Enterprise 계획에 각 웹 서버 노드 원격 분석을 전송 하는 각 날짜에 대 한 요금이 부과 됩니다. 연속 내보내기에 대규모로 toouse 하려는 경우 적합있지 않습니다.

[계획의 가격 책정 읽기 hello](https://azure.microsoft.com/pricing/details/application-insights/)합니다.

## <a name="how-much-is-it-costing"></a>비용은 어느 정도인가요?

* 열기 hello **기능 + 가격 책정** Application Insights 리소스에서 페이지. 최근 사용 현황에 대한 차트가 있습니다. 원하는 경우 데이터 볼륨 한도를 설정할 수 있습니다.
* 열기 hello [Azure 청구 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee 통해 대금 모든 리소스입니다.

## <a name="q14"></a>Application Insights에서 내 프로젝트를 어떻게 수정하나요?
hello 세부 정보는 프로젝트의 hello 유형에 따라 다릅니다. 웹 응용 프로그램의 경우:

* 이러한 파일 tooyour 프로젝트에 추가합니다.

  * ApplicationInsights.config
  * ai.js
* 다음 NuGet 패키지가 설치됩니다.

  * *Application Insights API* -hello 핵심 API
  * *웹 응용 프로그램에 대 한 application Insights API* -hello 서버에서 원격 분석 toosend 사용
  * *JavaScript 응용 프로그램에 대 한 application Insights API* -hello 클라이언트로부터 toosend 원격 분석 사용

    이러한 어셈블리를 포함 하는 hello 패키지:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* 항목 삽입 위치:

  * Web.config
  * packages.config
* (새 경우 프로젝트에 해당-있습니다 [Application Insights tooan 기존 프로젝트 추가][start]를 받아 주시 겠어요 toodo 수동으로.) 클라이언트와 서버 hello 코드 tooinitialize에 코드 조각을 삽입 hello Application Insights 리소스 ID를 사용 하 여 예를 들어 MVC 응용 프로그램에서 삽입 된 코드가 Views/Shared/_Layout.cshtml hello 마스터 페이지

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>이전 SDK 버전에서 업그레이드하려면 어떻게 해야 합니까?
Hello 참조 [릴리스 정보](app-insights-release-notes.md) hello SDK에 대 한 적절 한 응용 프로그램의 tooyour 유형입니다.

## <a name="update"></a>내 프로젝트에서 데이터를 보내는 Azure 리소스를 변경하려면 어떻게 해야 하나요?
솔루션 탐색기에서 `ApplicationInsights.config` 를 마우스 오른쪽 단추로 클릭하고 **Application Insights 업데이트**를 선택합니다. Azure의 hello 데이터 tooan 기존 또는 새 리소스를 보낼 수 있습니다. hello 업데이트 마법사 변경 내용을 hello hello 서버 SDK 데이터를 전송 하는 위치를 결정 하는 ApplicationInsights.config의 계측 키입니다. 선택 취소 하지 않으면 "업데이트 all", 웹 페이지에 표시 되는 hello 키도 변경 합니다.

## <a name="what-is-status-monitor"></a>상태 모니터란?

IIS 웹 서버 toohelp 프로그램에서 사용할 수 있는 데스크톱 응용 프로그램 웹 응용 프로그램에서 Application Insights를 구성 합니다. 원격 분석을 수집하지 않으며 앱을 구성하지 않는 경우 중지할 수 있습니다. 

[자세히 알아보기](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>어떤 원격 분석이 Application Insights에서 수집되나요?

서버 웹앱:

* HTTP 요청
* [종속성](app-insights-asp-net-dependencies.md). 에 대 한 호출: SQL 데이터베이스 HTTP은 tooexternal 서비스; 호출 Azure DB Cosmos, 테이블, blob 저장소 및 큐입니다. 
* [예외](app-insights-asp-net-exceptions.md) 및 스택 추적.
* [성능 카운터](app-insights-performance-counters.md) 사용 하는 경우- [상태 모니터](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) 또는 hello [Application Insights collectd 기록기](app-insights-java-collectd.md)합니다.
* 코딩하는 [사용자 지정 이벤트 및 메트릭](app-insights-api-custom-events-metrics.md).
* [추적 로그](app-insights-asp-net-trace-logs.md) hello 적절 한 수집기를 구성 하는 경우.

[클라이언트 웹 페이지](app-insights-javascript.md):

* [페이지 보기 수](app-insights-web-track-usage.md)
* 실행되는 스크립트의 [AJAX 호출](app-insights-asp-net-dependencies.md) 요청.
* 페이지 보기 로드 데이터
* 사용자 및 세션 수
* [인증된 사용자 ID](app-insights-api-custom-events-metrics.md#authenticated-users)

다른 원본(구성한 경우):

* [Azure 진단](app-insights-azure-diagnostics.md)
* [Docker 컨테이너](app-insights-docker.md)
* [가져오기 tooAnalytics 테이블](app-insights-analytics-import.md)
* [OMS(Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>일부 원격 분석을 필터링하거나 수정할 수 있나요?

예, hello 서버에서 작성할 수 있습니다.

* 원격 분석 프로세서 toofilter 또는 응용 프로그램에서 전송 하기 전에 속성 tooselected 원격 분석 항목을 추가 합니다.
* 원격 분석 이니셜라이저 tooadd 속성 tooall 항목의 원격 분석입니다.

[ASP.NET](app-insights-api-filtering-sampling.md) 또는 [Java](app-insights-java-filter-telemetry.md)에 대해 자세히 알아보세요.

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>도시, 국가 및 기타 지리적 위치 데이터는 어떻게 계산되나요?

Hello IP 주소 (IPv4 또는 IPv6)를 사용 하 여 hello 웹 클라이언트의 의견에 귀 [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/)합니다.

* 브라우저 원격 분석: hello 보낸 사람의 IP 주소를 수집 합니다.
* 서버 원격 분석: hello Application Insights 모듈 hello 클라이언트 IP 주소를 수집 합니다. `X-Forwarded-For`가 설정된 경우에는 수집되지 않습니다.

Hello를 구성할 수 있습니다 `ClientIpHeaderTelemetryInitializer` 다른 헤더에서 tootake hello IP 주소입니다. 일부 시스템의 예를 들어에서 이동할 프록시, 너무 로드 분산 장치, 또는 CDN`X-Originating-IP`합니다. [자세히 알아봅니다](http://apmtips.com/blog/2016/07/05/client-ip-address/).

있습니다 수 [Power BI를 사용 하 여](app-insights-export-power-bi.md) toodisplay 지도에서 요청 원격 분석 합니다.


## <a name="data"></a>Hello 포털에서 데이터를 보관 하는 기간 안전한가요?
[데이터 보존 및 개인 정보][data]를 살펴보십시오.

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>개인 식별이 가능한 정보 (PII) 발송 hello 원격 분석에서?

코드에서 이러한 데이터를 전송하는 경우 가능합니다. 스택 추적의 변수에 PII가 포함된 경우에도 전송될 수 있습니다. 개발 팀 위험 평가 tooensure PII 제대로 처리를 수행 해야 합니다. [데이터 보존 및 개인 정보](app-insights-data-retention-privacy.md)에 대해 자세히 알아보세요.

hello 마지막 8 진수 hello 클라이언트 웹 주소는 수집 후 too0 hello 포털에서 설정 항상 됩니다.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>내 iKey가 내 웹 페이지 원본에 표시됩니다. 

* 모니터링 솔루션에서 일반적으로 사용됩니다.
* 이 사용 되는 toosteal 데이터 일 수 없습니다.
* 이 사용 되는 tooskew 데이터 또는 트리거 경고 수 있습니다.
* 고객에게 이러한 문제가 발생한 경우는 없었습니다.

다음과 같이 할 수 있습니다.

* 클라이언트 데이터와 서버 데이터에 별도의 iKey(별도의 Application Insights 리소스) 두 개를 사용합니다. 또는
* 서버에서 실행 되는 프록시를 작성 하 고 hello 웹 클라이언트를 해당 프록시를 통해 데이터를 보냅니다.

## <a name="post"></a>진단 검색에서 POST 데이터를 어떻게 확인하나요?
자동으로 게시 데이터를 로깅하지 않습니다 것 이지만 TrackTrace 호출을 사용할 수 있습니다: hello 메시지 매개 변수에서 hello 데이터를 저장 합니다. 이에 필터링 할 수 없는 경우에 문자열 속성으로 hello 제한 보다 긴 크기 제한.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>단일 또는 여러 Application Insights 리소스를 사용해야 하나요?

단일 비즈니스 시스템의 모든 hello 구성 요소 또는 역할에 대해 단일 리소스를 사용 합니다. 개발, 테스트 및 릴리스 버전과 독립 응용 프로그램에 대해 별도의 리소스를 사용합니다.

* [Hello 토론 여기를 참조 하십시오.](app-insights-separate-resources.md)
* [예 - 작업자 및 웹 역할이 포함된 클라우드 서비스](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>동적으로 hello 계측 키를 변경 하는 방법

* [여기에서 토론 참조](app-insights-separate-resources.md)
* [예 - 작업자 및 웹 역할이 포함된 클라우드 서비스](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>계산 hello 사용자 및 세션 이란?

* hello JavaScript SDK는 hello 웹 클라이언트, tooidentify 반환 사용자 및 세션 쿠키 toogroup 작업에 사용자 쿠키를 설정 합니다.
* 수 없는 클라이언트 쪽 스크립트 이면 [hello 서버에서 쿠키를 설정](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/)합니다.
* 한 명의 실제 사용자가 특정 사이트를 다른 브라우저에서 사용하거나, in-private/incognito 검색을 통해 사용하거나, 다른 컴퓨터에서 사용하는 경우 두 번 이상 계산됩니다.
* 로그인 한 사용자 컴퓨터 및 브라우저 간에 tooidentify 호출을 너무 추가[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users)합니다.

## <a name="q17"></a> Application Insights의 모든 기능을 사용하도록 어떻게 설정하나요?
| 표시 내용 | 어떻게 tooget 것 | 원하는 이유 |
| --- | --- | --- |
| 가용성 차트 |[웹 테스트](app-insights-monitor-web-app-availability.md) |웹 앱이 작동 중인지 확인 |
| 서버 앱 성능: 응답시간. ... |[Application Insights tooyour 프로젝트 추가](app-insights-asp-net.md) 또는 [AI 상태 모니터 서버에 설치](app-insights-monitor-performance-live-website-now.md) (또는 사용자 고유의 코드를 너무 쓰기[종속성을 추적](app-insights-api-custom-events-metrics.md#trackdependency)) |성능 문제 검색 |
| 종속성 원격 분석 |[서버에 AI 상태 모니터 설치](app-insights-monitor-performance-live-website-now.md) |데이터베이스 또는 다른 외부 구성 요소의 문제 진단 |
| 예외에서 스택 추적 가져오기 |[TrackException 호출을 코드에 삽입](app-insights-asp-net-exceptions.md)(하지만 일부는 자동으로 보고됨) |예외 감지 및 진단 |
| 로그 추적 검색 |[로깅 어댑터 추가](app-insights-asp-net-trace-logs.md) |예외, 성능 문제 진단 |
| 클라이언트 사용 기본 사항: 페이지 보기, 세션,... |[웹 페이지의 JavaScript 이니셜라이저](app-insights-javascript.md) |사용 현황 분석 |
| 클라이언트 사용자 지정 메트릭 |[웹 페이지에서 추적 호출](app-insights-api-custom-events-metrics.md) |사용자 환경 향상 |
| 서버 사용자 지정 메트릭 |[서버에서 호출 추적](app-insights-api-custom-events-metrics.md) |비즈니스 인텔리전스 |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>이유는 hello 수를 검색 및 메트릭 차트 같지 않은?

[샘플링](app-insights-sampling.md) 원격 분석 항목 (요청, 사용자 지정 이벤트 및 등)는 실제로 앱 toohello 포털에서 전송 된 hello 수를 줄일 수 있습니다. 검색에 hello 실제로 수신 하는 항목 수가 표시 됩니다. 이벤트의 개수를 표시 하는 메트릭 차트를 hello 수가 원래 발생 한 이벤트를 볼 수 있습니다. 

전송되는 각 항목은 해당 항목이 나타내는 원래 이벤트의 수를 보여 주는 `itemCount` 속성을 전달합니다. tooobserve 작업에서 샘플링의 경우에서 실행할 수 있습니다이 쿼리 분석:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automation

### <a name="configuring-application-insights"></a>Application Insights 구성

Azure Resource Monitor를 통해 [PowerShell 스크립트를 작성](app-insights-powershell.md)하여 다음을 수행할 수 있습니다.

* Application Insights 리소스를 만들고 업데이트합니다.
* Hello 계획 가격 책정을 설정 합니다.
* Hello 계측 키를 가져옵니다.
* 메트릭 경고를 추가합니다.
* 가용성 테스트를 추가합니다.

메트릭 탐색기 보고서를 설정하거나 연속 내보내기를 설정할 수는 없습니다.

### <a name="querying-hello-telemetry"></a>Hello 원격 분석 쿼리

사용 하 여 hello [REST API](https://dev.applicationinsights.io/) toorun [분석](app-insights-analytics.md) 쿼리 합니다.

## <a name="how-can-i-set-an-alert-on-an-event"></a>이벤트에 대한 경고를 설정하려면 어떻게 해야 하나요?

Azure 경고는 메트릭에 대해서만 설정됩니다. 이벤트가 발생할 때마다 값 임계값을 초과하는 사용자 지정 메트릭을 만듭니다. 그런 다음 hello 메트릭을에 경고를 설정 합니다. : hello 메트릭을 어느 방향으로든; hello 임계값을 초과할 때마다 알림을 받게 됩니다 hello hello 초기 값 높거나 낮은; 인지에 관계 없이 첫 번째 무효화 될 때까지 알림을 가져올 수 없습니다. 몇 분의 대기 시간은 항상입니다.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Azure 웹앱과 Application Insights 간 데이터 전송 요금이 있나요?

* Azure 웹앱이 Application Insights 컬렉션 끝점이 있는 데이터 센터에서 호스트되는 경우 무료입니다. 
* 호스트 데이터 센터에 컬렉션 끝점이 없으면 앱의 원격 분석에 [Azure 발신 요금](https://azure.microsoft.com/pricing/details/bandwidth/)이 부과됩니다.

이 요금은 Application insights 리소스가 호스트되는 위치에 따라 달라지지 않습니다. 방금이 끝점의 hello 분포에 따라 달라 집니다.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>원격 분석 toohello Application Insights 포털을 보낼 수 있습니까?

이 Sdk를 사용 하 여 hello (app-insights-api-custom-events-metrics.md) SDK API를 사용 하는 것이 좋습니다. 다양 한 hello SDK의 테스트가 [플랫폼](app-insights-platforms.md)합니다. 이러한 SDK는 버퍼링, 압축, 제한, 다시 시도 등을 처리합니다. 그러나 hello [수집 스키마](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) 및 [끝점 프로토콜](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) 는 공용입니다.

## <a name="can-i-monitor-an-intranet-web-server"></a>인트라넷 웹 서버를 모니터링할 수 있나요?

다음은 두 가지 방법입니다.

### <a name="firewall-door"></a>방화벽 문

웹 서버 toosend tooour 끝점 https://dc.services.visualstudio.com:443 원격 분석 및 https://rt.services.visualstudio.com:443 허용 합니다. 

### <a name="proxy"></a>Proxy

ApplicationInsights.config에서이 설정 하 여 인트라넷의 서버 tooa 게이트웨이에서 트래픽을 라우팅합니다.

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

게이트웨이는 트래픽 toohttps://dc.services.visualstudio.com:443/v2/트랙 hello 라우팅해야 합니다.

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>인트라넷 서버에서 가용성 웹 테스트를 실행할 수 있나요?

우리의 [웹 테스트](app-insights-monitor-web-app-availability.md) 존재 hello 전 세계에 배포 되는 지점에서 실행 합니다. 두 가지 해결 방법이 있습니다.

* 방화벽 도어-요청 허용에서 tooyour 서버 [긴 hello 및 변경 가능 목록은 웹 테스트 에이전트](app-insights-ip-addresses.md)합니다.
* 사용자 고유의 코드 toosend 정기적으로 요청 tooyour 내에 서버에서 인트라넷을 작성 합니다. 이러한 목적으로 Visual Studio 웹 테스트를 실행할 수 있습니다. hello 테스터 tooApplication Insights hello TrackAvailability() API를 사용 하 여 hello 결과 보낼 수 있습니다.

## <a name="more-answers"></a>추가 대답
* [Application Insights 포럼](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md

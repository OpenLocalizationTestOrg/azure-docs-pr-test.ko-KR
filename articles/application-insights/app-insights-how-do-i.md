---
title: "aaaHow 할까요 Azure Application Insights에서 | Microsoft Docs"
description: "Application Insights의 FAQ"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Application Insights에서 다음을 수행하는 방법
## <a name="get-an-email-when-"></a>전자 메일을 받는 경우
### <a name="email-if-my-site-goes-down"></a>내 사이트가 다운되면 전자 메일로 알림
[가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 설정합니다.

### <a name="email-if-my-site-is-overloaded"></a>내 사이트가 과부하되면 전자 메일로 알림
[서버 응답 시간](app-insights-alerts.md) 에서 **경고**를 설정합니다. 1-2초 임계값이 적용됩니다.

![](./media/app-insights-how-do-i/030-server.png)

응용 프로그램이 오류 코드를 반환하여 부하의 흔적을 표시할 수도 있습니다. **실패한 요청**에 대한 경고를 설정합니다.

경고 tooset를 원하는 경우 **서버 예외**, toodo 있을 수 있습니다 [몇 가지 추가 설정이](app-insights-asp-net-exceptions.md) 주문 toosee 데이터에서입니다.

### <a name="email-on-exceptions"></a>예외에 대해 메일 보내기
1. [예외 모니터링 설정](app-insights-asp-net-exceptions.md)
2. [경고를 설정](app-insights-alerts.md) hello 예외에서 메트릭 계산

### <a name="email-on-an-event-in-my-app"></a>내 응용 프로그램에서 이벤트 발생 시 전자 메일로 알림
특정 이벤트가 발생할 때 tooget 전자 메일을 한다고 가정 하겠습니다. Application Insights는 이 기능을 직접 제공하지 않지만 [메트릭이 임계값에 도달했을 때](app-insights-alerts.md)경고를 보낼 수 있습니다.

경고는 사용자 지정 이벤트는 아니지만 [사용자 지정 메트릭](app-insights-api-custom-events-metrics.md#trackmetric)에서 설정할 수 있습니다. Hello 이벤트가 발생할 때 일부 코드 tooincrease 메트릭을 작성 합니다.

    telemetry.TrackMetric("Alarm", 10);

또는

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

경고는 두 개의 상태를 가지기 때문에 값이 있는 toosend 낮은 toohave 종료 hello 경고를 고려할 때:

    telemetry.TrackMetric("Alarm", 0.5);

차트를 만듭니다 [메트릭 탐색기](app-insights-metrics-explorer.md) toosee 경보가:

![](./media/app-insights-how-do-i/010-alarm.png)

이제 hello 메트릭을 mid 값 보다 짧은 기간 동안 발생 하는 경우 경고 toofire를 설정 합니다.

![](./media/app-insights-how-do-i/020-threshold.png)

평균 기간 toohello 최소 hello를 설정 합니다.

Hello 메트릭을 위에서 발생 하는 경우와 hello 임계값이 전자 메일을 얻을 수 있습니다.

일부 지점 tooconsider:

* 경고는 "경고" 및 "정상"의 두 상태가 있습니다. hello 상태 메트릭을 수신 되는 경우에 평가 됩니다.
* Hello 상태가 변경 될 때에 전자 메일이 전송 됩니다. 이 때문에 toosend 있는 높은 낮은 값이 모두 메트릭.
* hello 평균 tooevaluate hello 알림은 받은 hello 값의 hello 앞에 마침표를 통해 수행 됩니다. 되므로 전자 메일을 설정 하면 hello 기간 보다 더 자주 보낼 수 있습니다. 메트릭을 수신 될 때마다 발생 합니다.
* "경고" 및 "정상"에 메일이 전송 될 이후 tooconsider 다시 두 가지 상태 조건으로 원 샷 이벤트를 고려할 수도 있습니다. 예를 들어 "작업 완료" 이벤트 대신 조건이 "작업 진행 중 에서", 작업의 hello 시작 및 끝에서 전자 메일을 얻게.

### <a name="set-up-alerts-automatically"></a>자동 경고 설정
[PowerShell toocreate 새 경고를 사용 하 여](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>PowerShell tooManage Application Insights를 사용 하 여
* [새 리소스 만들기](app-insights-powershell-script-create-resource.md)
* [새 경고 만들기](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>서로 다른 버전에서 별도 원격 분석

* 앱에서 여러 역할: 단일 Application Insights 리소스 사용 및 cloud_Rolename 필터링. [자세히 알아보기](app-insights-monitor-multi-role-apps.md)
* 개발, 테스트 및 릴리스 버전 구분: 다른 Application Insights 리소스 사용. Web.config에서 hello 계측 키를 선택 합니다. [자세히 알아보기](app-insights-separate-resources.md)
* 빌드 버전 보고: 원격 분석 이니셜라이저를 사용하여 속성 추가. [자세히 알아보기](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>백엔드 서버 및 데스크톱 앱 모니터링
[사용 하 여 hello Windows Server SDK 모듈](app-insights-windows-desktop.md)합니다.

## <a name="visualize-data"></a>데이터 가상화
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>여러 앱의 메트릭이 있는 대시보드
* [메트릭 탐색기](app-insights-metrics-explorer.md)에서 차트를 사용자 지정하고 즐겨찾기에 저장합니다. Toohello Azure 대시보드에 고정 합니다.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>다른 원본 및 Application Insights의 데이터가 표시된 대시보드
* [원격 분석 tooPower BI 내보내기](app-insights-export-power-bi.md)합니다.

또는

* SharePoint를 대시보드로 사용하여 SharePoint 웹 파트에 데이터를 표시 합니다. [연속 내보내기 및 스트림 분석 tooexport tooSQL 사용할](app-insights-code-sample-export-sql-stream-analytics.md)합니다.  PowerView tooexamine hello 데이터베이스를 사용 하 고 대 한 PowerView SharePoint 웹 파트를 만듭니다.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>익명 또는 인증된 사용자 필터링
사용자가 로그인 하는 경우에 hello을 설정할 수 있습니다 [사용자 id를 인증](app-insights-api-custom-events-metrics.md#authenticated-users)합니다. 이 작업은 자동으로 수행되지 않습니다.

그런 다음 다음을 수행할 수 있습니다.

* 특정 사용자 ID 검색

![](./media/app-insights-how-do-i/110-search.png)

* 메트릭 tooeither 익명 또는 인증 된 사용자 필터링

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>속성 이름 또는 값 수정
[필터](app-insights-api-filtering-sampling.md#filtering)를 만듭니다. 이렇게 하면 수정 하거나 사용자 앱 tooApplication Insights에서에서 전송 하기 전에 원격 분석을 필터링 합니다.

## <a name="list-specific-users-and-their-usage"></a>특정 사용자와 그 사용 방법을 나열 
원한다 면 너무[특정 사용자에 대 한 검색](#search-specific-users), hello를 설정할 수 있습니다 [사용자 id를 인증](app-insights-api-custom-events-metrics.md#authenticated-users)합니다.

사용자가 보는 페이지, 로그인 빈도 등과 같은 데이터와 사용자 목록이 필요한 경우 두 가지 옵션이 있습니다.

* [인증 된 사용자 id 집합](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa 데이터베이스 내보내기](app-insights-code-sample-export-sql-stream-analytics.md) 및 사용 하 여 적합 한 도구 tooanalyze 사용자 데이터입니다.
* 소수의 사용자를 설정한 경우 사용자 지정 이벤트 또는 관심 있는 hello 데이터 hello 메트릭 값 또는 이벤트 이름 및 속성으로 설정 hello 사용자 id로 사용 하는 메트릭을 보냅니다. tooanalyze 페이지 뷰 hello 표준 JavaScript trackPageView 호출을 대체 합니다. tooanalyze 서버 쪽 원격 분석 된 원격 분석 이니셜라이저 tooadd hello 사용자 id tooall 서버 원격 분석을 사용 합니다. 그런 다음 필터 및 세그먼트 메트릭 및 hello 사용자 id에 대 한 검색 수 있습니다.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>내 앱 tooApplication Insights에서에서 트래픽을 줄이기
* [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), 이러한 hello 성능 카운터 수집기 필요 없는 모든 모듈을 사용 하지 않도록 설정 합니다.
* 사용 하 여 [샘플링 및 필터링](app-insights-api-filtering-sampling.md) hello SDK에 있습니다.
* 웹 페이지에서 모든 페이지 보기에 대해 보고 된 Ajax 호출 hello 수를 제한 합니다. 다음 스크립트 조각을 hello에 `instrumentationKey:...` , 삽입: `,maxAjaxCallsPerView:3` (또는 인원이).
* 사용 중인 경우 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), hello 결과 보내기 전에 메트릭 값의 일괄 처리의 hello 집계를 계산 합니다. 이를 제공하는 TrackMetric() 오버로드가 있습니다.

[가격 책정 및 할당량](app-insights-pricing.md)에 대해 자세히 확인합니다.

## <a name="disable-telemetry"></a>원격 분석 사용 안 함

너무**동적으로 중지 하 고 시작** 컬렉션과 hello 서버에서 원격 분석 전송을 hello:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



너무**선택한 표준 수집기를 해제** -예: 성능 카운터, HTTP 요청 또는 종속성-삭제 하거나 hello 관련 줄의 주석 처리 [ApplicationInsights.config](app-insights-api-custom-events-metrics.md)합니다. 그렇게 할 수, 예를 들어 toosend TrackRequest 자신만 데이터를 원하는 경우.

## <a name="view-system-performance-counters"></a>시스템 성능 카운터 보기
Hello 메트릭 메트릭 탐색기에 표시할 수는 시스템 성능 카운터 집합이 있습니다. 이름이 **서버** 인 미리 정의된 블레이드에서 그중 몇 가지를 표시합니다.

![Application Insights 리소스를 열고서버 클릭](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>성능 카운터 데이터가 없는 경우
* **IIS 서버** . [상태 모니터를 설치합니다](app-insights-monitor-performance-live-website-now.md).
* **Azure 웹 사이트** - 성능 카운터는 아직 지원되지 않습니다. 여러 가지 메트릭을 hello Azure 웹 사이트 제어판의 표준 작업으로 가져올 수 있습니다.
* **Unix 서버** - [collectd 설치](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay 성능 카운터
* 첫째, [새 차트를 추가](app-insights-metrics-explorer.md) 볼 경우 hello 카운터 hello 기본 집합에 제공 했습니다.
* 그렇지 않으면 [hello 성능 카운터 모듈에 의해 수집 된 hello 카운터 toohello 집합 추가](app-insights-performance-counters.md)합니다.

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
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="cbf54-103">Application Insights에서 다음을 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="cbf54-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="cbf54-104">전자 메일을 받는 경우</span><span class="sxs-lookup"><span data-stu-id="cbf54-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="cbf54-105">내 사이트가 다운되면 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="cbf54-105">Email if my site goes down</span></span>
<span data-ttu-id="cbf54-106">[가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="cbf54-107">내 사이트가 과부하되면 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="cbf54-107">Email if my site is overloaded</span></span>
<span data-ttu-id="cbf54-108">[서버 응답 시간](app-insights-alerts.md) 에서 **경고**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="cbf54-109">1-2초 임계값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="cbf54-110">응용 프로그램이 오류 코드를 반환하여 부하의 흔적을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="cbf54-111">**실패한 요청**에 대한 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="cbf54-112">경고 tooset를 원하는 경우 **서버 예외**, toodo 있을 수 있습니다 [몇 가지 추가 설정이](app-insights-asp-net-exceptions.md) 주문 toosee 데이터에서입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="cbf54-113">예외에 대해 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="cbf54-113">Email on exceptions</span></span>
1. [<span data-ttu-id="cbf54-114">예외 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="cbf54-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="cbf54-115">[경고를 설정](app-insights-alerts.md) hello 예외에서 메트릭 계산</span><span class="sxs-lookup"><span data-stu-id="cbf54-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="cbf54-116">내 응용 프로그램에서 이벤트 발생 시 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="cbf54-116">Email on an event in my app</span></span>
<span data-ttu-id="cbf54-117">특정 이벤트가 발생할 때 tooget 전자 메일을 한다고 가정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="cbf54-118">Application Insights는 이 기능을 직접 제공하지 않지만 [메트릭이 임계값에 도달했을 때](app-insights-alerts.md)경고를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="cbf54-119">경고는 사용자 지정 이벤트는 아니지만 [사용자 지정 메트릭](app-insights-api-custom-events-metrics.md#trackmetric)에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="cbf54-120">Hello 이벤트가 발생할 때 일부 코드 tooincrease 메트릭을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="cbf54-121">또는</span><span class="sxs-lookup"><span data-stu-id="cbf54-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="cbf54-122">경고는 두 개의 상태를 가지기 때문에 값이 있는 toosend 낮은 toohave 종료 hello 경고를 고려할 때:</span><span class="sxs-lookup"><span data-stu-id="cbf54-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="cbf54-123">차트를 만듭니다 [메트릭 탐색기](app-insights-metrics-explorer.md) toosee 경보가:</span><span class="sxs-lookup"><span data-stu-id="cbf54-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="cbf54-124">이제 hello 메트릭을 mid 값 보다 짧은 기간 동안 발생 하는 경우 경고 toofire를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="cbf54-125">평균 기간 toohello 최소 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="cbf54-126">Hello 메트릭을 위에서 발생 하는 경우와 hello 임계값이 전자 메일을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="cbf54-127">일부 지점 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="cbf54-127">Some points tooconsider:</span></span>

* <span data-ttu-id="cbf54-128">경고는 "경고" 및 "정상"의 두 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="cbf54-129">hello 상태 메트릭을 수신 되는 경우에 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="cbf54-130">Hello 상태가 변경 될 때에 전자 메일이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="cbf54-131">이 때문에 toosend 있는 높은 낮은 값이 모두 메트릭.</span><span class="sxs-lookup"><span data-stu-id="cbf54-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="cbf54-132">hello 평균 tooevaluate hello 알림은 받은 hello 값의 hello 앞에 마침표를 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="cbf54-133">되므로 전자 메일을 설정 하면 hello 기간 보다 더 자주 보낼 수 있습니다. 메트릭을 수신 될 때마다 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="cbf54-134">"경고" 및 "정상"에 메일이 전송 될 이후 tooconsider 다시 두 가지 상태 조건으로 원 샷 이벤트를 고려할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="cbf54-135">예를 들어 "작업 완료" 이벤트 대신 조건이 "작업 진행 중 에서", 작업의 hello 시작 및 끝에서 전자 메일을 얻게.</span><span class="sxs-lookup"><span data-stu-id="cbf54-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="cbf54-136">자동 경고 설정</span><span class="sxs-lookup"><span data-stu-id="cbf54-136">Set up alerts automatically</span></span>
[<span data-ttu-id="cbf54-137">PowerShell toocreate 새 경고를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cbf54-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="cbf54-138">PowerShell tooManage Application Insights를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cbf54-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="cbf54-139">새 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="cbf54-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="cbf54-140">새 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="cbf54-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="cbf54-141">서로 다른 버전에서 별도 원격 분석</span><span class="sxs-lookup"><span data-stu-id="cbf54-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="cbf54-142">앱에서 여러 역할: 단일 Application Insights 리소스 사용 및 cloud_Rolename 필터링.</span><span class="sxs-lookup"><span data-stu-id="cbf54-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="cbf54-143">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="cbf54-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="cbf54-144">개발, 테스트 및 릴리스 버전 구분: 다른 Application Insights 리소스 사용.</span><span class="sxs-lookup"><span data-stu-id="cbf54-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="cbf54-145">Web.config에서 hello 계측 키를 선택 합니다. [자세히 알아보기](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="cbf54-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="cbf54-146">빌드 버전 보고: 원격 분석 이니셜라이저를 사용하여 속성 추가.</span><span class="sxs-lookup"><span data-stu-id="cbf54-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="cbf54-147">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="cbf54-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="cbf54-148">백엔드 서버 및 데스크톱 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="cbf54-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="cbf54-149">[사용 하 여 hello Windows Server SDK 모듈](app-insights-windows-desktop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="cbf54-150">데이터 가상화</span><span class="sxs-lookup"><span data-stu-id="cbf54-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="cbf54-151">여러 앱의 메트릭이 있는 대시보드</span><span class="sxs-lookup"><span data-stu-id="cbf54-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="cbf54-152">[메트릭 탐색기](app-insights-metrics-explorer.md)에서 차트를 사용자 지정하고 즐겨찾기에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="cbf54-153">Toohello Azure 대시보드에 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="cbf54-154">다른 원본 및 Application Insights의 데이터가 표시된 대시보드</span><span class="sxs-lookup"><span data-stu-id="cbf54-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="cbf54-155">[원격 분석 tooPower BI 내보내기](app-insights-export-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="cbf54-156">또는</span><span class="sxs-lookup"><span data-stu-id="cbf54-156">Or</span></span>

* <span data-ttu-id="cbf54-157">SharePoint를 대시보드로 사용하여 SharePoint 웹 파트에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="cbf54-158">[연속 내보내기 및 스트림 분석 tooexport tooSQL 사용할](app-insights-code-sample-export-sql-stream-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="cbf54-159">PowerView tooexamine hello 데이터베이스를 사용 하 고 대 한 PowerView SharePoint 웹 파트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="cbf54-160">익명 또는 인증된 사용자 필터링</span><span class="sxs-lookup"><span data-stu-id="cbf54-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="cbf54-161">사용자가 로그인 하는 경우에 hello을 설정할 수 있습니다 [사용자 id를 인증](app-insights-api-custom-events-metrics.md#authenticated-users)합니다. 이 작업은 자동으로 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="cbf54-162">그런 다음 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-162">You can then:</span></span>

* <span data-ttu-id="cbf54-163">특정 사용자 ID 검색</span><span class="sxs-lookup"><span data-stu-id="cbf54-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="cbf54-164">메트릭 tooeither 익명 또는 인증 된 사용자 필터링</span><span class="sxs-lookup"><span data-stu-id="cbf54-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="cbf54-165">속성 이름 또는 값 수정</span><span class="sxs-lookup"><span data-stu-id="cbf54-165">Modify property names or values</span></span>
<span data-ttu-id="cbf54-166">[필터](app-insights-api-filtering-sampling.md#filtering)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="cbf54-167">이렇게 하면 수정 하거나 사용자 앱 tooApplication Insights에서에서 전송 하기 전에 원격 분석을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="cbf54-168">특정 사용자와 그 사용 방법을 나열 </span><span class="sxs-lookup"><span data-stu-id="cbf54-168">List specific users and their usage</span></span>
<span data-ttu-id="cbf54-169">원한다 면 너무[특정 사용자에 대 한 검색](#search-specific-users), hello를 설정할 수 있습니다 [사용자 id를 인증](app-insights-api-custom-events-metrics.md#authenticated-users)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="cbf54-170">사용자가 보는 페이지, 로그인 빈도 등과 같은 데이터와 사용자 목록이 필요한 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="cbf54-171">[인증 된 사용자 id 집합](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa 데이터베이스 내보내기](app-insights-code-sample-export-sql-stream-analytics.md) 및 사용 하 여 적합 한 도구 tooanalyze 사용자 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="cbf54-172">소수의 사용자를 설정한 경우 사용자 지정 이벤트 또는 관심 있는 hello 데이터 hello 메트릭 값 또는 이벤트 이름 및 속성으로 설정 hello 사용자 id로 사용 하는 메트릭을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="cbf54-173">tooanalyze 페이지 뷰 hello 표준 JavaScript trackPageView 호출을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="cbf54-174">tooanalyze 서버 쪽 원격 분석 된 원격 분석 이니셜라이저 tooadd hello 사용자 id tooall 서버 원격 분석을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="cbf54-175">그런 다음 필터 및 세그먼트 메트릭 및 hello 사용자 id에 대 한 검색 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="cbf54-176">내 앱 tooApplication Insights에서에서 트래픽을 줄이기</span><span class="sxs-lookup"><span data-stu-id="cbf54-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="cbf54-177">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), 이러한 hello 성능 카운터 수집기 필요 없는 모든 모듈을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="cbf54-178">사용 하 여 [샘플링 및 필터링](app-insights-api-filtering-sampling.md) hello SDK에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="cbf54-179">웹 페이지에서 모든 페이지 보기에 대해 보고 된 Ajax 호출 hello 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="cbf54-180">다음 스크립트 조각을 hello에 `instrumentationKey:...` , 삽입: `,maxAjaxCallsPerView:3` (또는 인원이).</span><span class="sxs-lookup"><span data-stu-id="cbf54-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="cbf54-181">사용 중인 경우 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), hello 결과 보내기 전에 메트릭 값의 일괄 처리의 hello 집계를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="cbf54-182">이를 제공하는 TrackMetric() 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="cbf54-183">[가격 책정 및 할당량](app-insights-pricing.md)에 대해 자세히 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="cbf54-184">원격 분석 사용 안 함
</span><span class="sxs-lookup"><span data-stu-id="cbf54-184">Disable telemetry</span></span>
<span data-ttu-id="cbf54-185">너무**동적으로 중지 하 고 시작** 컬렉션과 hello 서버에서 원격 분석 전송을 hello:</span><span class="sxs-lookup"><span data-stu-id="cbf54-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="cbf54-186">너무**선택한 표준 수집기를 해제** -예: 성능 카운터, HTTP 요청 또는 종속성-삭제 하거나 hello 관련 줄의 주석 처리 [ApplicationInsights.config](app-insights-api-custom-events-metrics.md)합니다. 그렇게 할 수, 예를 들어 toosend TrackRequest 자신만 데이터를 원하는 경우.</span><span class="sxs-lookup"><span data-stu-id="cbf54-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="cbf54-187">시스템 성능 카운터 보기</span><span class="sxs-lookup"><span data-stu-id="cbf54-187">View system performance counters</span></span>
<span data-ttu-id="cbf54-188">Hello 메트릭 메트릭 탐색기에 표시할 수는 시스템 성능 카운터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="cbf54-189">이름이 **서버** 인 미리 정의된 블레이드에서 그중 몇 가지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Application Insights 리소스를 열고서버 클릭](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="cbf54-191">성능 카운터 데이터가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="cbf54-191">If you see no performance counter data</span></span>
* <span data-ttu-id="cbf54-192">**IIS 서버** .</span><span class="sxs-lookup"><span data-stu-id="cbf54-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="cbf54-193">[상태 모니터를 설치합니다](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="cbf54-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="cbf54-194">**Azure 웹 사이트** - 성능 카운터는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="cbf54-195">여러 가지 메트릭을 hello Azure 웹 사이트 제어판의 표준 작업으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="cbf54-196">**Unix 서버** - [collectd 설치](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="cbf54-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="cbf54-197">toodisplay 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="cbf54-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="cbf54-198">첫째, [새 차트를 추가](app-insights-metrics-explorer.md) 볼 경우 hello 카운터 hello 기본 집합에 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="cbf54-199">그렇지 않으면 [hello 성능 카운터 모듈에 의해 수집 된 hello 카운터 toohello 집합 추가](app-insights-performance-counters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbf54-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>

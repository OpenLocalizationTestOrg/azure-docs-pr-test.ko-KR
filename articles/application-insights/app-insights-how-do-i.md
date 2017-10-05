---
title: "Azure Application Insights에서 어떻게 할까요? | Microsoft Docs"
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="79d55-103">Application Insights에서 다음을 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="79d55-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="79d55-104">전자 메일을 받는 경우</span><span class="sxs-lookup"><span data-stu-id="79d55-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="79d55-105">내 사이트가 다운되면 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="79d55-105">Email if my site goes down</span></span>
<span data-ttu-id="79d55-106">[가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="79d55-107">내 사이트가 과부하되면 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="79d55-107">Email if my site is overloaded</span></span>
<span data-ttu-id="79d55-108">[서버 응답 시간](app-insights-alerts.md) 에서 **경고**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="79d55-109">1-2초 임계값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="79d55-110">응용 프로그램이 오류 코드를 반환하여 부하의 흔적을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="79d55-111">**실패한 요청**에 대한 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="79d55-112">**서버 예외**에 대한 경고를 설정하기 위해 데이터를 확인하는 데 [일부 추가 설치](app-insights-asp-net-exceptions.md) 를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="79d55-113">예외에 대해 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="79d55-113">Email on exceptions</span></span>
1. [<span data-ttu-id="79d55-114">예외 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="79d55-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="79d55-115">[경고 설정](app-insights-alerts.md) </span><span class="sxs-lookup"><span data-stu-id="79d55-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="79d55-116">내 응용 프로그램에서 이벤트 발생 시 전자 메일로 알림</span><span class="sxs-lookup"><span data-stu-id="79d55-116">Email on an event in my app</span></span>
<span data-ttu-id="79d55-117">특정 이벤트가 발생할 때 전자 메일을 받으려 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="79d55-118">Application Insights는 이 기능을 직접 제공하지 않지만 [메트릭이 임계값에 도달했을 때](app-insights-alerts.md)경고를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="79d55-119">경고는 사용자 지정 이벤트는 아니지만 [사용자 지정 메트릭](app-insights-api-custom-events-metrics.md#trackmetric)에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="79d55-120">이벤트 발생 시 메트릭 향상을 위한 몇 가지 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="79d55-121">또는</span><span class="sxs-lookup"><span data-stu-id="79d55-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="79d55-122">경고에는 두 상태가 있기 때문에 경고 종료를 고려할 때 낮은 값을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="79d55-123">[메트릭 탐색기](app-insights-metrics-explorer.md) 에서 차트를 만들어 경고를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="79d55-124">이제 메트릭이 짧은 기간 동안 중간 값 위로 상승하면 발생하는 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="79d55-125">평균 기간을 최소로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="79d55-126">메트릭이 임계값 위와 아래로 가면 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="79d55-127">몇 가지 고려할 점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-127">Some points to consider:</span></span>

* <span data-ttu-id="79d55-128">경고는 "경고" 및 "정상"의 두 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="79d55-129">상태는 메트릭 수신 시에만 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="79d55-130">상태가 변경될 때만 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="79d55-131">이 때문에 높은 값과 낮은 값의 메트릭을 모두 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="79d55-132">경고를 평가하기 위해 이전 기간 동안 수신한 값에서 평균을 취합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="79d55-133">이 작업은 메트릭이 수신될 때마다 발생하므로 설정한 기간보다 더 자주 전자 메일이 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="79d55-134">"경고" 및 "정상"에서 모두 전자 메일을 보내므로 원샷 이벤트를 2상태 조건으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="79d55-135">예를 들어, "작업 완료" 이벤트 대신, 작업 시작과 종료 시 전자 메일을 받는 "작업 진행 중"  조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="79d55-136">자동 경고 설정</span><span class="sxs-lookup"><span data-stu-id="79d55-136">Set up alerts automatically</span></span>
[<span data-ttu-id="79d55-137">PowerShell을 사용하여 새 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="79d55-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="79d55-138">PowerShell을 사용하여 Application Insights 관리</span><span class="sxs-lookup"><span data-stu-id="79d55-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="79d55-139">새 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="79d55-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="79d55-140">새 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="79d55-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="79d55-141">서로 다른 버전에서 별도 원격 분석</span><span class="sxs-lookup"><span data-stu-id="79d55-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="79d55-142">앱에서 여러 역할: 단일 Application Insights 리소스 사용 및 cloud_Rolename 필터링.</span><span class="sxs-lookup"><span data-stu-id="79d55-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="79d55-143">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="79d55-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="79d55-144">개발, 테스트 및 릴리스 버전 구분: 다른 Application Insights 리소스 사용.</span><span class="sxs-lookup"><span data-stu-id="79d55-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="79d55-145">web.config에서 계측 키를 선택합니다. [자세히 알아보기](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="79d55-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="79d55-146">빌드 버전 보고: 원격 분석 이니셜라이저를 사용하여 속성 추가.</span><span class="sxs-lookup"><span data-stu-id="79d55-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="79d55-147">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="79d55-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="79d55-148">백엔드 서버 및 데스크톱 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="79d55-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="79d55-149">[Windows Server SDK 모듈을 사용합니다](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="79d55-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="79d55-150">데이터 가상화</span><span class="sxs-lookup"><span data-stu-id="79d55-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="79d55-151">여러 앱의 메트릭이 있는 대시보드</span><span class="sxs-lookup"><span data-stu-id="79d55-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="79d55-152">[메트릭 탐색기](app-insights-metrics-explorer.md)에서 차트를 사용자 지정하고 즐겨찾기에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="79d55-153">Azure 대시보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="79d55-154">다른 원본 및 Application Insights의 데이터가 표시된 대시보드</span><span class="sxs-lookup"><span data-stu-id="79d55-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="79d55-155">[Power BI에 원격 분석을 내보냅니다](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="79d55-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="79d55-156">또는</span><span class="sxs-lookup"><span data-stu-id="79d55-156">Or</span></span>

* <span data-ttu-id="79d55-157">SharePoint를 대시보드로 사용하여 SharePoint 웹 파트에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="79d55-158">[연속 내보내기 및 스트림 분석을 사용하여 SQL로 내보냅니다](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="79d55-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="79d55-159">PowerView를 사용하여 데이터베이스를 검사하고 PowerView에 대한 SharePoint 웹 파트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="79d55-160">익명 또는 인증된 사용자 필터링</span><span class="sxs-lookup"><span data-stu-id="79d55-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="79d55-161">사용자가 로그인할 경우 [인증된 사용자 ID](app-insights-api-custom-events-metrics.md#authenticated-users)를 설정할 수 있습니다. 이 작업은 자동으로 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="79d55-162">그런 다음 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-162">You can then:</span></span>

* <span data-ttu-id="79d55-163">특정 사용자 ID 검색</span><span class="sxs-lookup"><span data-stu-id="79d55-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="79d55-164">익명 또는 인증된 사용자에 대해 메트릭 필터링</span><span class="sxs-lookup"><span data-stu-id="79d55-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="79d55-165">속성 이름 또는 값 수정</span><span class="sxs-lookup"><span data-stu-id="79d55-165">Modify property names or values</span></span>
<span data-ttu-id="79d55-166">[필터](app-insights-api-filtering-sampling.md#filtering)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="79d55-167">그러면 원격 분석을 수정하거나 필터링한 후 앱에서 Application Insights로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="79d55-168">특정 사용자와 그 사용 방법을 나열 </span><span class="sxs-lookup"><span data-stu-id="79d55-168">List specific users and their usage</span></span>
<span data-ttu-id="79d55-169">[특정 사용자만 검색](#search-specific-users)하려는 경우 [인증된 사용자 ID](app-insights-api-custom-events-metrics.md#authenticated-users)를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="79d55-170">사용자가 보는 페이지, 로그인 빈도 등과 같은 데이터와 사용자 목록이 필요한 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="79d55-171">[인증된 사용자 ID를 설정하고](app-insights-api-custom-events-metrics.md#authenticated-users) [데이터베이스로 내보내고](app-insights-code-sample-export-sql-stream-analytics.md) 적합한 도구를 사용하여 사용자 데이터를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="79d55-172">사용자 수가 적은 경우, 관심이 있는 데이터를 사용하는 사용자 지정 이벤트나 메트릭을 메트릭 값 또는 이벤트 이름 형태로 보내고 사용자 ID를 속성으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="79d55-173">페이지 보기를 분석하려면 표준 JavaScript trackPageView 호출을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="79d55-174">서버 측 원격 분석을 분석하려면 원격 분석 이니셜라이저를 사용하여 사용자 ID를 모든 서버 원격 분석에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="79d55-175">그런 다음 메트릭과 사용자 ID에 대한 검색을 필터링 및 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="79d55-176">Application Insights에 대한 내 앱의 트래픽 줄이기</span><span class="sxs-lookup"><span data-stu-id="79d55-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="79d55-177">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 성능 카운터 수집기 등 필요하지 않은 모듈을 모두 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="79d55-178">SDK에서 [샘플링 및 필터링](app-insights-api-filtering-sampling.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="79d55-179">웹 페이지에서 모든 페이지 뷰에 대해 보고되는 Ajax 호출 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="79d55-180">스크립트 조각에서 `instrumentationKey:...` 뒤에 `,maxAjaxCallsPerView:3`(또는 적절한 숫자)을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="79d55-181">[TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)을 사용하는 경우 결과를 보내기 전에 메트릭 값의 배치 집계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="79d55-182">이를 제공하는 TrackMetric() 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="79d55-183">[가격 책정 및 할당량](app-insights-pricing.md)에 대해 자세히 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="79d55-184">원격 분석 사용 안 함
</span><span class="sxs-lookup"><span data-stu-id="79d55-184">Disable telemetry</span></span>
<span data-ttu-id="79d55-185">서버로부터 원격 분석의 컬렉션 및 전송을 **동적으로 중지 및 시작** 하려면:</span><span class="sxs-lookup"><span data-stu-id="79d55-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="79d55-186">**선택한 표준 수집기(예: 성능 카운터, HTTP 요청 또는 종속성)를 사용하지 않도록 설정** 하려면 [ApplicationInsights.config](app-insights-api-custom-events-metrics.md)에서 관련 줄을 삭제하거나 주석으로 처리합니다. 사용자 고유의 TrackRequest 데이터를 전송하려는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="79d55-187">시스템 성능 카운터 보기</span><span class="sxs-lookup"><span data-stu-id="79d55-187">View system performance counters</span></span>
<span data-ttu-id="79d55-188">메트릭 탐색기에서 표시할 수 있는 메트릭 중에는 시스템 성능 카운터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="79d55-189">이름이 **서버** 인 미리 정의된 블레이드에서 그중 몇 가지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Application Insights 리소스를 열고서버 클릭](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="79d55-191">성능 카운터 데이터가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="79d55-191">If you see no performance counter data</span></span>
* <span data-ttu-id="79d55-192">**IIS 서버** .</span><span class="sxs-lookup"><span data-stu-id="79d55-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="79d55-193">[상태 모니터를 설치합니다](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="79d55-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="79d55-194">**Azure 웹 사이트** - 성능 카운터는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="79d55-195">Azure 웹 사이트 제어판의 표준 부분으로 몇 가지 메트릭을 가져올  수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="79d55-196">**Unix 서버** - [collectd 설치](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="79d55-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="79d55-197">더 많은 성능 카운터를 표시하려면</span><span class="sxs-lookup"><span data-stu-id="79d55-197">To display more performance counters</span></span>
* <span data-ttu-id="79d55-198">먼저 [새 차트를 추가하고](app-insights-metrics-explorer.md) 제공한 기본 집합에 카운터가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79d55-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="79d55-199">없으면 [성능 카운터 모듈에서 수집한 집합에 카운터를 추가합니다](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="79d55-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>

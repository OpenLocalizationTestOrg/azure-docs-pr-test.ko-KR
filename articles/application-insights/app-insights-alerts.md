---
title: "Azure Application Insights에서 경고 설정 | Microsoft Docs"
description: "느린 응답 시간, 예외 및 웹앱의 기타 성능 또는 사용 변경에 대한 알림을 받습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: c8386ffc5d68260eeb75edf7efb77db1163dcef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="set-alerts-in-application-insights"></a><span data-ttu-id="3d3c8-103">Application Insights에서 경고 설정</span><span class="sxs-lookup"><span data-stu-id="3d3c8-103">Set Alerts in Application Insights</span></span>
<span data-ttu-id="3d3c8-104">[Azure Application Insights][start]는 웹앱의 성능 및 사용 메트릭이 변경되면 사용자에게 경고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-104">[Azure Application Insights][start] can alert you to changes in performance or usage metrics in your web app.</span></span> 

<span data-ttu-id="3d3c8-105">Application Insights는 [다양한 플랫폼][platforms]에서 라이브 앱을 모니터링하여 성능 문제를 진단하고 사용 패턴을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] to help you diagnose performance issues and understand usage patterns.</span></span>

<span data-ttu-id="3d3c8-106">경고의 종류는 세 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-106">There are three kinds of alerts:</span></span>

* <span data-ttu-id="3d3c8-107">**메트릭 경고**는 메트릭이 응답 시간, 예외 수, CPU 사용량 또는 페이지 보기 등의 임계값을 일정 기간 동안 초과하면 그 사실을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span></span> 
* <span data-ttu-id="3d3c8-108">[**웹 테스트**][availability]는 인터넷에서 사이트를 사용할 수 없거나 응답 속도가 느려지면 그 사실을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-108">[**Web tests**][availability] tell you when your site is unavailable on the internet, or responding slowly.</span></span> <span data-ttu-id="3d3c8-109">[자세한 정보][availability].</span><span class="sxs-lookup"><span data-stu-id="3d3c8-109">[Learn more][availability].</span></span>
* <span data-ttu-id="3d3c8-110">[**사전 진단**](app-insights-proactive-diagnostics.md)은 비정상적인 성능 패턴에 대해 알려 주기 위해 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically to notify you about unusual performance patterns.</span></span>

<span data-ttu-id="3d3c8-111">이 문서에서는 메트릭 경고에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-111">We focus on metric alerts in this article.</span></span>

## <a name="set-a-metric-alert"></a><span data-ttu-id="3d3c8-112">메트릭 경고 설정</span><span class="sxs-lookup"><span data-stu-id="3d3c8-112">Set a Metric alert</span></span>
<span data-ttu-id="3d3c8-113">경고 규칙 블레이드를 연 다음 추가 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-113">Open the Alert rules blade, and then use the add button.</span></span> 

![경고 규칙 블레이드에서 경고 추가를 선택합니다.](./media/app-insights-alerts/01-set-metric.png)

* <span data-ttu-id="3d3c8-116">다른 속성에 앞서 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-116">Set the resource before the other properties.</span></span> <span data-ttu-id="3d3c8-117">**"(구성 요소)" 리소스 선택** 성능 또는 사용 메트릭에 대한 경고를 설정하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-117">**Choose the "(components)" resource** if you want to set alerts on performance or usage metrics.</span></span>
* <span data-ttu-id="3d3c8-118">경고에 입력하는 이름은 리소스 그룹(응용 프로그램 아님) 내에서 고유한 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-118">The name that you give to the alert must be unique within the resource group (not just your application).</span></span>
* <span data-ttu-id="3d3c8-119">임계값을 입력하라는 단위에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-119">Be careful to note the units in which you're asked to enter the threshold value.</span></span>
* <span data-ttu-id="3d3c8-120">"메일 소유자..." 확인란을 선택하면 이 리소스 그룹에 액세스하는 모든 사용자에게 메일로 경고가 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-120">If you check the box "Email owners...", alerts are sent by email to everyone who has access to this resource group.</span></span> <span data-ttu-id="3d3c8-121">사용자 집합을 확장하려면 [리소스 그룹 또는 구독](app-insights-resources-roles-access-control.md) (리소스 아님)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-121">To expand this set of people, add them to the [resource group or subscription](app-insights-resources-roles-access-control.md) (not the resource).</span></span>
* <span data-ttu-id="3d3c8-122">"추가 메일"을 지정하면 "메일 소유자..." 확인란의 선택 여부와 상관없이 이러한 개인 또는 그룹에게 경고가 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-122">If you specify "Additional emails", alerts are sent to those individuals or groups (whether or not you checked the "email owners..." box).</span></span> 
* <span data-ttu-id="3d3c8-123">경고에 응답하는 웹앱을 설정한 경우 [웹후크 주소](../monitoring-and-diagnostics/insights-webhooks-alerts.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds to alerts.</span></span> <span data-ttu-id="3d3c8-124">경고가 활성화될 때 및 해결될 때 모두 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-124">It is called both when the alert is Activated and when it is Resolved.</span></span> <span data-ttu-id="3d3c8-125">그러나 현재 쿼리 매개 변수는 웹후크 속성으로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-125">(But note that at present, query parameters are not passed through as webhook properties.)</span></span>
* <span data-ttu-id="3d3c8-126">블레이드 맨 위에 있는 단추를 참조하여 경고를 사용 또는 사용 안 함으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-126">You can Disable or Enable the alert: see the buttons at the top of the blade.</span></span>

<span data-ttu-id="3d3c8-127">*경고 추가 단추가 보이지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="3d3c8-127">*I don't see the Add Alert button.*</span></span> 

* <span data-ttu-id="3d3c8-128">조직 계정을 사용 중이신가요?</span><span class="sxs-lookup"><span data-stu-id="3d3c8-128">Are you using an organizational account?</span></span> <span data-ttu-id="3d3c8-129">이 응용 프로그램 리소스에 소유자 또는 참가자 액세스가 가능하면 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-129">You can set alerts if you have owner or contributor access to this application resource.</span></span> <span data-ttu-id="3d3c8-130">Access Control 블레이드를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-130">Take a look at the Access Control blade.</span></span> <span data-ttu-id="3d3c8-131">[액세스 제어에 대해 자세히 알아보세요][roles].</span><span class="sxs-lookup"><span data-stu-id="3d3c8-131">[Learn about access control][roles].</span></span>

> [!NOTE]
> <span data-ttu-id="3d3c8-132">경고 블레이드에 [사전 진단](app-insights-proactive-failure-diagnostics.md) 경고 설정이 이미 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-132">In the alerts blade, you see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="3d3c8-133">자동 경고는 특정 메트릭, 요청 실패율을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-133">The automatic alert monitors one particular metric, request failure rate.</span></span> <span data-ttu-id="3d3c8-134">사전 경고를 사용하지 않으려는 경우가 아니면 요청 실패율에 대한 자체 경고를 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-134">Unless you decide to disable the proactive alert, you don't need to set your own alert on request failure rate.</span></span> 
> 
> 

## <a name="see-your-alerts"></a><span data-ttu-id="3d3c8-135">경고 보기</span><span class="sxs-lookup"><span data-stu-id="3d3c8-135">See your alerts</span></span>
<span data-ttu-id="3d3c8-136">알림 상태가 비활성 및 활성 간에 변경될 때 전자 메일이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-136">You get an email when an alert changes state between inactive and active.</span></span> 

<span data-ttu-id="3d3c8-137">각 알림의 현재 상태는 알림 규칙 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-137">The current state of each alert is shown in the Alert rules blade.</span></span>

<span data-ttu-id="3d3c8-138">경고 드롭다운에 최신 활동에 대한 요약이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-138">There's a summary of recent activity in the alerts drop-down:</span></span>

![경고 드롭다운](./media/app-insights-alerts/010-alert-drop.png)

<span data-ttu-id="3d3c8-140">상태 변경 내역은 활동 로그에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-140">The history of state changes is in the Activity Log:</span></span>

![개요 블레이드에서 설정, 감사 로그를 클릭합니다.](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a><span data-ttu-id="3d3c8-142">경고 작동 방식</span><span class="sxs-lookup"><span data-stu-id="3d3c8-142">How alerts work</span></span>
* <span data-ttu-id="3d3c8-143">경고에는 "활성화되지 않음", "활성화됨", "해결됨"의 세 가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span></span> <span data-ttu-id="3d3c8-144">활성화됨은 마지막으로 평가되었을 때 지정한 조건이 true였음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-144">Activated means the condition you specified was true, when it was last evaluated.</span></span>
* <span data-ttu-id="3d3c8-145">경고 상태가 변경되면 알림이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-145">A notification is generated when an alert changes state.</span></span> <span data-ttu-id="3d3c8-146">(경고를 만들었을 때 이미 경고 조건이 true인 경우 조건이 false가 될 때까지 알림이 발생되지 않을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3d3c8-146">(If the alert condition was already true when you created the alert, you might not get a notification until the condition goes false.)</span></span>
* <span data-ttu-id="3d3c8-147">메일 상자를 선택했거나 메일 주소를 제공한 경우 각 알림은 메일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-147">Each notification generates an email if you checked the emails box, or provided email addresses.</span></span> <span data-ttu-id="3d3c8-148">알림 드롭다운 목록에서 찾아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-148">You can also look at the Notifications drop-down list.</span></span>
* <span data-ttu-id="3d3c8-149">메트릭이 도착할 때마다 경고가 평가되고 그렇지 않은 경우는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-149">An alert is evaluated each time a metric arrives, but not otherwise.</span></span>
* <span data-ttu-id="3d3c8-150">평가는 이전 기간에 대한 메트릭을 집계한 다음 임계값과 비교하여 새 상태를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-150">The evaluation aggregates the metric over the preceding period, and then compares it to the threshold to determine the new state.</span></span>
* <span data-ttu-id="3d3c8-151">선택하는 기간으로 메트릭이 집계되는 간격이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-151">The period that you choose specifies the interval over which metrics are aggregated.</span></span> <span data-ttu-id="3d3c8-152">기간은 경고가 평가되는 빈도에는 영향을 주지 않습니다. 이는 메트릭 도착 빈도에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-152">It doesn't affect how often the alert is evaluated: that depends on the frequency of arrival of metrics.</span></span>
* <span data-ttu-id="3d3c8-153">일정 시간 동안 특정 메트릭에 대해 데이터가 도착하지 않는 경우 해당 간격은 메트릭 탐색기의 차트와 경고 평가에 다른 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-153">If no data arrives for a particular metric for some time, the gap has different effects on alert evaluation and on the charts in metric explorer.</span></span> <span data-ttu-id="3d3c8-154">메트릭 탐색기에서 데이터가 차트의 샘플링 간격보다 오랫동안 표시되지 않는 경우 차트 값에는 0이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-154">In metric explorer, if no data is seen for longer than the chart's sampling interval, the chart shows a value of 0.</span></span> <span data-ttu-id="3d3c8-155">하지만 동일한 메트릭에 따른 경고는 재평가되지 않으며 경고의 상태는 변경되지 않고 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-155">But an alert based on the same metric is not be reevaluated, and the alert's state remains unchanged.</span></span> 
  
    <span data-ttu-id="3d3c8-156">마침내 데이터가 도착하면 차트는 0이 아닌 값으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-156">When data eventually arrives, the chart jumps back to a non-zero value.</span></span> <span data-ttu-id="3d3c8-157">경고는 지정된 기간 동안 사용 가능한 데이터에 따라 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-157">The alert evaluates based on the data available for the period you specified.</span></span> <span data-ttu-id="3d3c8-158">새 데이터 요소를 해당 기간에 하나만 사용할 수 있는 경우 집계는 해당 데이터 요소만 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-158">If the new data point is the only one available in the period, the aggregate is based just on that data point.</span></span>
* <span data-ttu-id="3d3c8-159">경고는 긴 기간을 설정한 경우에도 경고와 정상 상태 사이에서 자주 깜박거릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span></span> <span data-ttu-id="3d3c8-160">메트릭 값이 임계값 주위를 가리키는 경우 이런 현상이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-160">This can happen if the metric value hovers around the threshold.</span></span> <span data-ttu-id="3d3c8-161">임계값에는 이력이 없습니다. 경고로 전환되는 것과 정상으로 전환되는 것이 같은 값에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-161">There is no hysteresis in the threshold: the transition to alert happens at the same value as the transition to healthy.</span></span>

## <a name="what-are-good-alerts-to-set"></a><span data-ttu-id="3d3c8-162">어떤 경고를 설정하면 좋은가요?</span><span class="sxs-lookup"><span data-stu-id="3d3c8-162">What are good alerts to set?</span></span>
<span data-ttu-id="3d3c8-163">응용 프로그램에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-163">It depends on your application.</span></span> <span data-ttu-id="3d3c8-164">처음에는 경고를 너무 많이 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-164">To start with, it's best not to set too many metrics.</span></span> <span data-ttu-id="3d3c8-165">일단 앱이 실행되는 동안 메트릭 차트를 살펴보면서 정상적으로 작동할 때의 상태를 숙지합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-165">Spend some time looking at your metric charts while your app is running, to get a feel for how it behaves normally.</span></span> <span data-ttu-id="3d3c8-166">이렇게 하면 성능을 개선하는 방법을 찾는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-166">This practice helps you find ways to improve its performance.</span></span> <span data-ttu-id="3d3c8-167">그런 다음 메트릭이 정상 영역을 벗어나면 알려주는 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-167">Then set up alerts to tell you when the metrics go outside the normal zone.</span></span> 

<span data-ttu-id="3d3c8-168">다음은 많은 사람들이 사용하는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-168">Popular alerts include:</span></span>

* <span data-ttu-id="3d3c8-169">[브라우저 메트릭][client], 특히 브라우저 **페이지 로드 시간**은 웹 응용 프로그램에 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span></span> <span data-ttu-id="3d3c8-170">페이지에 스크립트가 많은 경우 **브라우저 예외**를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-170">If your page has many scripts, you should look for **browser exceptions**.</span></span> <span data-ttu-id="3d3c8-171">이러한 메트릭 및 경고를 가져오려면 [웹 페이지 모니터링][client]을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-171">In order to get these metrics and alerts, you have to set up [web page monitoring][client].</span></span>
* <span data-ttu-id="3d3c8-172">서버 쪽 웹 응용 프로그램에 대한 **서버 응답 시간**.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-172">**Server response time** for the server side of web applications.</span></span> <span data-ttu-id="3d3c8-173">경고 설정 외에도 이 메트릭을 주시하여 메트릭이 불균형적으로 변하고 요청 속도가 빠른지 살펴보는 것이 좋습니다. 변형은 앱에 리소스가 부족하다는 의미일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-173">As well as setting up alerts, keep an eye on this metric to see if it varies disproportionately with high request rates: variation might indicate that your app is running out of resources.</span></span> 
* <span data-ttu-id="3d3c8-174">**서버 예외** 를 보려면 일부 [추가 설치](app-insights-asp-net-exceptions.md)작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-174">**Server exceptions** - to see them, you have to do some [additional setup](app-insights-asp-net-exceptions.md).</span></span>

<span data-ttu-id="3d3c8-175">[자동 관리 실패율 진단](app-insights-proactive-failure-diagnostics.md)은 앱이 오류 코드로 요청에 응답하는 속도를 자동으로 모니터링한다는 것을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3d3c8-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor the rate at which your app responds to requests with failure codes.</span></span> 

## <a name="automation"></a><span data-ttu-id="3d3c8-176">자동화</span><span class="sxs-lookup"><span data-stu-id="3d3c8-176">Automation</span></span>
* [<span data-ttu-id="3d3c8-177">PowerShell을 사용하여 경고 설정 자동화</span><span class="sxs-lookup"><span data-stu-id="3d3c8-177">Use PowerShell to automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="3d3c8-178">Webhook를 사용하여 경고에 대한 응답 자동화</span><span class="sxs-lookup"><span data-stu-id="3d3c8-178">Use webhooks to automate responding to alerts</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a><span data-ttu-id="3d3c8-179">비디오</span><span class="sxs-lookup"><span data-stu-id="3d3c8-179">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a><span data-ttu-id="3d3c8-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3d3c8-180">See also</span></span>
* [<span data-ttu-id="3d3c8-181">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="3d3c8-181">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="3d3c8-182">경고 설정 자동화</span><span class="sxs-lookup"><span data-stu-id="3d3c8-182">Automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="3d3c8-183">사전 진단</span><span class="sxs-lookup"><span data-stu-id="3d3c8-183">Proactive diagnostics</span></span>](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md


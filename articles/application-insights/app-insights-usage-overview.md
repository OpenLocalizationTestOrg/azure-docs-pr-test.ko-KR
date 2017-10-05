---
title: "Azure Application Insights를 사용한 웹 응용 프로그램의 사용 현황 분석 | Microsoft Docs"
description: "어떤 사용자가 웹앱으로 어떤 작업을 수행하는지 이해합니다."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="93e29-103">Application Insights를 사용한 웹 응용 프로그램의 사용 현황 분석</span><span class="sxs-lookup"><span data-stu-id="93e29-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="93e29-104">가장 인기 있는 웹앱의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="93e29-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="93e29-105">사용자가 앱으로 이러한 목표를 달성하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="93e29-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="93e29-106">특정 지점에서 나갔다가 나중에 돌아오나요?</span><span class="sxs-lookup"><span data-stu-id="93e29-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="93e29-107">[Azure Application Insights](app-insights-overview.md)는 사람들이 사용자의 웹앱을 사용하는 방식을 잘 이해할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="93e29-108">앱을 업데이트할 때마다 사용자들에게 얼마나 적절한지 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="93e29-109">이러한 지식을 바탕으로 다음 개발 주기에 대해 데이터 중심의 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="93e29-110">앱에서 원격 분석 보내기</span><span class="sxs-lookup"><span data-stu-id="93e29-110">Send telemetry from your app</span></span>

<span data-ttu-id="93e29-111">앱 서버 코드와 웹 페이지에 모두 Application Insights를 설치하여 최상의 환경을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="93e29-112">앱의 클라이언트 및 서버 구성 요소는 분석을 위해 Azure Portal로 원격 분석을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="93e29-113">**서버 코드:** [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) 또는 [기타](app-insights-platforms.md) 앱에 적합한 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="93e29-114">*서버 코드를 설치하지 않으려면 [Azure Application Insights 리소스를 만들기만](app-insights-create-new-resource.md) 하면 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="93e29-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="93e29-115">**웹 페이지 코드:** [Azure Portal](https://portal.azure.com)을 열고 앱에 대한 Application Insights 리소스를 연 다음 **시작하기 > Monitor and Diagnose Client-Side(클라이언트 쪽 모니터링 및 진단)**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![마스터 웹 페이지의 머리글에 스크립트를 복사합니다.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="93e29-117">**원격 분석 가져오기:** 몇 분 동안 디버그 모드에서 프로젝트를 실행한 다음 Application Insights의 개요 블레이드에서 결과를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="93e29-118">앱을 게시하여 앱의 성능을 모니터링하고 사용자가 앱으로 수행하는 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="93e29-119">원격 분석에 사용자 및 세션 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="93e29-120">시간이 지남에 따라 사용자를 추적하려면 Application Insights는 식별하는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="93e29-121">이벤트 도구는 사용자 ID 또는 세션 ID가 필요 없는 유일한 사용 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="93e29-122">[여기](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context)에서 이러한 ID를 보내기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="93e29-123">사용 현황 인구 통계 및 통계 탐색</span><span class="sxs-lookup"><span data-stu-id="93e29-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="93e29-124">사람들이 사용자의 앱을 사용하는 경우, 가장 큰 관심을 갖는 페이지, 사용자가 있는 위치 및 사용하는 브라우저 및 운영 체제를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="93e29-125">사용자 및 세션 보고서는 페이지 또는 사용자 지정 이벤트를 기준으로 데이터를 필터링하고 위치, 환경 및 페이지 등의 속성으로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="93e29-126">필터를 직접 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-126">You can also add your own filters.</span></span>

![사용자](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="93e29-128">오른쪽의 자세한 정보에는 데이터 집합에서 주목할 만한 패턴이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="93e29-129">**사용자** 보고서는 선택한 기간 내에 페이지에 액세스하는 고유한 사용자 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="93e29-130">(사용자는 쿠키를 사용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="93e29-131">누군가가 다른 브라우저 또는 클라이언트 컴퓨터를 사용하여 사이트에 액세스하는 경우 두 번 이상 계산됩니다.)</span><span class="sxs-lookup"><span data-stu-id="93e29-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="93e29-132">**세션** 보고서는 사이트에 액세스하는 사용자 세션의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="93e29-133">세션은 30분 이상의 비활동 기간마다 종료되는 사용자의 활동 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="93e29-134">사용자, 세션 및 이벤트 도구에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="93e29-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="93e29-135">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="93e29-135">Page views</span></span>

<span data-ttu-id="93e29-136">사용 현황 블레이드에서 페이지 보기 타일을 클릭하여 가장 인기 있는 페이지에 대한 분석 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![개요 블레이드에서 페이지 보기 차트 클릭](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="93e29-138">위의 예제는 게임 웹 사이트에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-138">The example above is from a games web site.</span></span> <span data-ttu-id="93e29-139">차트에서 바로 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="93e29-140">사용량은 지난 주보다 개선되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="93e29-141">검색 엔진 최적화에 대해 생각해볼 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="93e29-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="93e29-142">테니스가 가장 인기 있는 게임 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="93e29-143">이 페이지의 향상된 기능을 집중적으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="93e29-144">평균적으로 사용자는 주당 약 세 번 테니스 페이지를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="93e29-145">사용자보다 세션이 약 3배 더 많습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="93e29-146">대부분의 사용자는 미국 근무 주간 및 근무 시간에 사이트를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="93e29-147">웹 페이지에 “빠른 숨기기” 단추를 제공해야 할 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="93e29-148">차트의 [주석](app-insights-annotations.md)은 웹 사이트의 새 버전이 배포된 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="93e29-149">최근 배포는 사용 현황에 크게 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="93e29-150">페이지 보기 원격 분석에서 사이트가 보내는 사용자 지정 속성별로 분할하는 것과 같이, 사이트에 대한 트래픽을 좀 더 자세히 조사하고 싶으면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="93e29-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="93e29-151">Application Insights 리소스 메뉴에서 **이벤트** 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="93e29-152">이 도구를 사용하면 다양한 필터링, 코호트 및 분할 옵션에 따라 앱에서 전송된 페이지 보기 및 사용자 지정 이벤트 수를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="93e29-153">"사용한 사람" 드롭다운에서 "페이지 보기"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="93e29-154">"분할 기준" 드롭다운에서 페이지 보기 원격 분석을 분할할 기준 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="93e29-155">재방문 주기 - 다시 찾아온 사용자는 몇 명이나 되나요?</span><span class="sxs-lookup"><span data-stu-id="93e29-155">Retention - how many users come back?</span></span>

<span data-ttu-id="93e29-156">재방문 주기는 특정 시간 버킷 동안 일부 비즈니스 작업을 수행한 사용자의 코호트를 기준으로 사용자가 해당 앱을 다시 사용하는 빈도를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="93e29-157">사용자가 다시 찾아오게 만드는 특정 기능 이해</span><span class="sxs-lookup"><span data-stu-id="93e29-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="93e29-158">실제 사용자 데이터에 따라 가설 세우기</span><span class="sxs-lookup"><span data-stu-id="93e29-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="93e29-159">재방문 주기가 제품에서 문제가 되는지 여부 확인</span><span class="sxs-lookup"><span data-stu-id="93e29-159">Determine whether retention is a problem in your product</span></span> 

![보존](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="93e29-161">상단의 재방문 주기 컨트롤을 사용하여 재방문 주기를 계산할 특정 이벤트 및 시간 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="93e29-162">중간에 표시되는 그래프는 지정된 시간 범위별로 전반적인 재방문 주기 비율을 시각적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="93e29-163">하단의 그래프는 지정된 기간 내의 개별 재방문 주기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="93e29-164">이 수준의 세부 정보를 사용하면 사용자가 수행하는 작업과 다시 방문한 사용자에게 영향을 미칠 수 있는 요인을 좀 더 자세히 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="93e29-165">재방문 주기 도구에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="93e29-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="93e29-166">사용자 지정 비즈니스 이벤트</span><span class="sxs-lookup"><span data-stu-id="93e29-166">Custom business events</span></span>

<span data-ttu-id="93e29-167">사용자가 웹앱으로 수행하는 작업을 명확하게 이해하려는 경우 사용자 지정 이벤트를 로깅하는 코드 줄을 삽입하면 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="93e29-168">이러한 이벤트는 특정 단추 클릭과 같은 자세한 사용자 작업부터 구매하기나 게임에서 이기기 등과 같은 좀 더 중요한 비즈니스 이벤트에 이르기까지 모든 사항을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="93e29-169">경우에 따라 페이지 보기에 유용한 이벤트가 표시될 수 있지만 일반적으로는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="93e29-170">사용자는 제품 페이지를 열기만 하고 제품을 구입하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="93e29-171">특정 비즈니스 이벤트를 사용하여 사이트를 통한 사용자의 진행 상황을 차트로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="93e29-172">다양한 옵션에 대한 사용자의 선호도를 알아내고 사이트를 나가거나 어려움을 느끼는 경우를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="93e29-173">이러한 지식을 바탕으로 개발 백로그에서 우선 순위를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="93e29-174">이벤트는 웹 페이지에 로깅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="93e29-175">또는 웹앱의 서버 쪽에 로깅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="93e29-176">포털에서 검사할 때 이벤트를 필터링하거나 분할할 수 있도록 이러한 이벤트에 속성 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="93e29-177">또한 익명 사용자 ID와 같은 표준 속성 집합이 각 이벤트에 추가되므로 개별 사용자의 활동 시퀀스를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="93e29-178">[사용자 지정 이벤트](app-insights-api-custom-events-metrics.md#trackevent) 및 [속성](app-insights-api-custom-events-metrics.md#properties)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="93e29-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="93e29-179">이벤트 분석 및 분할</span><span class="sxs-lookup"><span data-stu-id="93e29-179">Slice and dice events</span></span>

<span data-ttu-id="93e29-180">사용자, 세션 및 이벤트 도구에서 사용자, 이벤트 이름 및 속성별로 사용자 지정 이벤트를 분석 및 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="93e29-181">![사용자](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="93e29-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="93e29-182">앱을 사용하여 원격 분석 디자인</span><span class="sxs-lookup"><span data-stu-id="93e29-182">Design the telemetry with the app</span></span>

<span data-ttu-id="93e29-183">앱의 각 기능을 디자인할 때 사용자를 대상으로 앱의 성공 여부를 측정하는 방법을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="93e29-184">기록해야 하는 비즈니스 이벤트를 결정하고 해당 이벤트에 대한 추적 호출을 처음부터 앱에 코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="93e29-185">A | B 테스트</span><span class="sxs-lookup"><span data-stu-id="93e29-185">A | B Testing</span></span>
<span data-ttu-id="93e29-186">기능의 어느 변형이 보다 성공적인지 알 수 없는 경우, 다른 사용자가 각각 접근할 수 있도록 하여 둘 다 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="93e29-187">각각의 성공 여부를 측정한 다음 통합 버전으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="93e29-188">이 기술의 경우 사용자 앱의 각 버전이 전송한 모든 원격 분석에 고유 속성 값을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="93e29-189">활성화된 TelemetryContext에서 속성을 정의하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="93e29-190">이러한 기본 속성은 사용자 지정 메시지뿐 아니라 표준 원격 분석도 응용 프로그램이 전송하는 모든 원격 분석 메시지에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="93e29-191">Application Insights 포털에서 속성 값에 대해 데이터를 필터링하고 분할하여 다른 버전과 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="93e29-192">이렇게 하려면 [원격 분석 이니셜라이저를 설정](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer)합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="93e29-193">Global.asax.cs 같은 웹앱 이니셜라이저에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="93e29-194">새로운 모든 TelemetryClient는 사용자가 지정하는 속성 값을 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="93e29-195">개별 원격 분석 이벤트는 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e29-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93e29-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93e29-196">Next steps</span></span>
   - [<span data-ttu-id="93e29-197">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="93e29-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="93e29-198">깔때기</span><span class="sxs-lookup"><span data-stu-id="93e29-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="93e29-199">보존</span><span class="sxs-lookup"><span data-stu-id="93e29-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="93e29-200">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="93e29-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="93e29-201">통합 문서</span><span class="sxs-lookup"><span data-stu-id="93e29-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="93e29-202">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="93e29-202">Add user context</span></span>](app-insights-usage-send-user-context.md)

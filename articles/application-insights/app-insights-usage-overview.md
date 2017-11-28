---
title: "Azure Application Insights를 사용한 웹 응용 프로그램에 대 한 aaaUsage 분석 | Microsoft docs"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="ae46f-103">Application Insights를 사용한 웹 응용 프로그램의 사용 현황 분석</span><span class="sxs-lookup"><span data-stu-id="ae46f-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="ae46f-104">가장 인기 있는 웹앱의 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ae46f-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="ae46f-105">사용자가 앱으로 이러한 목표를 달성하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="ae46f-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="ae46f-106">특정 지점에서 나갔다가 나중에 돌아오나요?</span><span class="sxs-lookup"><span data-stu-id="ae46f-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="ae46f-107">[Azure Application Insights](app-insights-overview.md)는 사람들이 사용자의 웹앱을 사용하는 방식을 잘 이해할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="ae46f-108">앱을 업데이트할 때마다 사용자들에게 얼마나 적절한지 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="ae46f-109">이러한 지식을 바탕으로 다음 개발 주기에 대해 데이터 중심의 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="ae46f-110">앱에서 원격 분석 보내기</span><span class="sxs-lookup"><span data-stu-id="ae46f-110">Send telemetry from your app</span></span>

<span data-ttu-id="ae46f-111">Application Insights를 응용 프로그램 서버 코드와 웹 페이지에서 설치 하 여 hello 최고의 사용 환경을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="ae46f-112">hello 클라이언트와 서버 구성 요소가 응용 프로그램의 원격 분석 백 toohello 분석을 위해 Azure 포털을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="ae46f-113">**서버 코드:** 설치에 대 한 적절 한 모듈 hello 프로그램 [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), 또는 [다른](app-insights-platforms.md) 앱.</span><span class="sxs-lookup"><span data-stu-id="ae46f-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="ae46f-114">*Tooinstall 서버 코드를 원하지 않습니까? [Azure Application Insights 리소스를 만들기만](app-insights-create-new-resource.md) 하면 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="ae46f-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="ae46f-115">**웹 페이지 코드:** 열려 hello [Azure 포털](https://portal.azure.com), 응용 프로그램에 대 한 hello Application Insights 리소스를 열고 **시작 > 모니터 및 진단 클라이언트 쪽**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![마스터 웹 페이지의 hello 헤드에 hello 스크립트를 복사 합니다.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="ae46f-117">**원격 분석 가져오기:** 몇 분 동안 디버그 모드에서 프로젝트를 실행 한 다음에서 Application Insights 개요 블레이드에 hello에서 결과 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="ae46f-118">응용 프로그램의 성능 앱 toomonitor를 게시 하 고 사용자가 수행 하는 앱과 함께 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="ae46f-119">원격 분석에 사용자 및 세션 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="ae46f-120">시간이 지남에 따라 tootrack 사용자, Application Insights 필요한 방식으로 tooidentify 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="ae46f-121">이 도구는 hello 이벤트 hello 사용자 ID 또는 id가 세션 ID가 필요 없는 유일한 사용 도구</span><span class="sxs-lookup"><span data-stu-id="ae46f-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="ae46f-122">[여기](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context)에서 이러한 ID를 보내기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="ae46f-123">사용 현황 인구 통계 및 통계 탐색</span><span class="sxs-lookup"><span data-stu-id="ae46f-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="ae46f-124">사람들이 사용자의 앱을 사용하는 경우, 가장 큰 관심을 갖는 페이지, 사용자가 있는 위치 및 사용하는 브라우저 및 운영 체제를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="ae46f-125">hello 사용자와 세션 보고서는 페이지 또는 사용자 지정 이벤트 데이터를 필터링 및 위치, 환경 및 페이지의 속성으로으로 나누는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="ae46f-126">필터를 직접 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-126">You can also add your own filters.</span></span>

![사용자](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="ae46f-128">오른쪽 hello에 대 한 통찰력 hello 데이터 집합이 주목할 만한 패턴 지적 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="ae46f-129">hello **사용자** 보고서는 선택한 시간 기간 내에서 페이지에 액세스 하는 고유한 사용자 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="ae46f-130">(사용자는 쿠키를 사용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="ae46f-131">누군가가 다른 브라우저 또는 클라이언트 컴퓨터를 사용하여 사이트에 액세스하는 경우 두 번 이상 계산됩니다.)</span><span class="sxs-lookup"><span data-stu-id="ae46f-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="ae46f-132">hello **세션** 보고서 사이트에 액세스 하는 사용자 세션의 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="ae46f-133">세션은 30분 이상의 비활동 기간마다 종료되는 사용자의 활동 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="ae46f-134">Hello 사용자, 세션 및 이벤트 도구에 자세히</span><span class="sxs-lookup"><span data-stu-id="ae46f-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="ae46f-135">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="ae46f-135">Page views</span></span>

<span data-ttu-id="ae46f-136">Hello 사용 블레이드에서 가장 인기 있는 페이지에 대 한 분석을 통해 hello 페이지 보기 타일 tooget 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Hello 개요 블레이드에서 hello 페이지 뷰 차트를 클릭 합니다.](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="ae46f-138">게임 웹 사이트에서 위의 hello 예제가입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-138">hello example above is from a games web site.</span></span> <span data-ttu-id="ae46f-139">Hello 차트에서 즉시 았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="ae46f-140">사용 현황 지난 주 hello에서는 개선 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="ae46f-141">검색 엔진 최적화에 대해 생각해볼 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="ae46f-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="ae46f-142">테니스는 hello 가장 인기 있는 게임 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="ae46f-143">추가 개선 toothis 페이지에 대해 중점적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="ae46f-144">평균적으로 사용자가 페이지를 방문 hello 테니스 세 번 약 일주일.</span><span class="sxs-lookup"><span data-stu-id="ae46f-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="ae46f-145">사용자보다 세션이 약 3배 더 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="ae46f-146">대부분의 사용자가 근무 시간 및 hello 미국 작업 주간 hello 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="ae46f-147">아마도 hello 웹 페이지에 "빠른 숨기기" 단추를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="ae46f-148">hello [주석](app-insights-annotations.md) hello 차트 hello 웹 사이트의 새 버전 배포 된 경우를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="ae46f-149">Hello 최근 배포 중에 사용량이 많은 영향을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="ae46f-150">경우에 어떻게 tooinvestigate hello 트래픽 tooyour 사이트에서 사이트의 페이지 보기 원격 분석에 보내는 사용자 지정 속성에 의해 분할와 같은 좀 더 자세하게 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="ae46f-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="ae46f-151">열기 hello **이벤트** hello Application Insights 리소스 메뉴의 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="ae46f-152">이 도구를 사용하면 다양한 필터링, 코호트 및 분할 옵션에 따라 앱에서 전송된 페이지 보기 및 사용자 지정 이벤트 수를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="ae46f-153">드롭다운 "가 사용 된" hello, "Any 페이지 보기"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="ae46f-154">Hello "분할" 드롭다운에 있는 toosplit 하 여 페이지 보기 원격 분석 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="ae46f-155">재방문 주기 - 다시 찾아온 사용자는 몇 명이나 되나요?</span><span class="sxs-lookup"><span data-stu-id="ae46f-155">Retention - how many users come back?</span></span>

<span data-ttu-id="ae46f-156">보존은 얼마나 자주 사용자에 게 반환 toouse 패 거리 들은 특정 시간 버킷의 하는 동안 일부 비즈니스 작업을 수행 하는 사용자에 따라 앱을 이해 하도록 도와 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="ae46f-157">특정 기능 하면 사용자가 다른 항목 보다 더 많은 toocome 백 이해</span><span class="sxs-lookup"><span data-stu-id="ae46f-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="ae46f-158">실제 사용자 데이터에 따라 가설 세우기</span><span class="sxs-lookup"><span data-stu-id="ae46f-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="ae46f-159">재방문 주기가 제품에서 문제가 되는지 여부 확인</span><span class="sxs-lookup"><span data-stu-id="ae46f-159">Determine whether retention is a problem in your product</span></span> 

![보존](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="ae46f-161">hello 보존 컨트롤 위에 표시 하면 toodefine 특정 이벤트 및 범위 toocalculate 보존 시간을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="ae46f-162">hello 그래프 hello 중간에 시각적 표시를 제공 hello의 지정 된 hello 시간 범위 내에서 전체 보존 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="ae46f-163">hello 아래쪽에 hello 그래프는 지정 된 기간에 개별 보존을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="ae46f-164">이 정보의 수준의 사용 하면 어떤 사용자가 수행 하는 toounderstand 및 어떤 반환 사용자 보다 자세한 세분성에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="ae46f-165">Hello 보존 도구에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ae46f-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="ae46f-166">사용자 지정 비즈니스 이벤트</span><span class="sxs-lookup"><span data-stu-id="ae46f-166">Custom business events</span></span>

<span data-ttu-id="ae46f-167">웹 앱을 사용 하 여 tooget 사용자가 명확 하 게 이해 수행할에 유용한 tooinsert 줄 코드 toolog 사용자 지정 이벤트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="ae46f-168">이러한 이벤트는 특정 단추, 게임 우세한 하거나 제품을 구매 하는 등 중요 한 비즈니스 이벤트 toomore 클릭과 같은 자세한 사용자 작업에서 아무 것도 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="ae46f-169">경우에 따라 페이지 보기에 유용한 이벤트가 표시될 수 있지만 일반적으로는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="ae46f-170">사용자는 hello 제품을 구입 하지 않고도 제품 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="ae46f-171">특정 비즈니스 이벤트를 사용하여 사이트를 통한 사용자의 진행 상황을 차트로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="ae46f-172">다양한 옵션에 대한 사용자의 선호도를 알아내고 사이트를 나가거나 어려움을 느끼는 경우를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="ae46f-173">이 정보를 개발 백로그에 hello 우선 순위에 대해 합리적인된 결정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="ae46f-174">Hello 웹 페이지에 이벤트가 기록 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="ae46f-175">또는 hello 웹 응용 프로그램의 hello 서버 측:</span><span class="sxs-lookup"><span data-stu-id="ae46f-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="ae46f-176">속성 값 toothese 이벤트를 필터링 하거나 hello 포털에서 검사 하면 hello 이벤트를 분할할 수 있도록 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="ae46f-177">표준 속성 집합이 tootrace hello 일련의 개별 사용자의 작업 수 있는 익명 사용자 ID와 같은 연결 된 tooeach 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="ae46f-178">[사용자 지정 이벤트](app-insights-api-custom-events-metrics.md#trackevent) 및 [속성](app-insights-api-custom-events-metrics.md#properties)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ae46f-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="ae46f-179">이벤트 분석 및 분할</span><span class="sxs-lookup"><span data-stu-id="ae46f-179">Slice and dice events</span></span>

<span data-ttu-id="ae46f-180">Hello 사용자, 세션 및 이벤트 도구에서 분할 수 있으며 사용자, 이벤트 이름 및 속성에 의해 사용자 지정 이벤트를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="ae46f-181">![사용자](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="ae46f-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="ae46f-182">Hello 앱 디자인 hello 원격 분석</span><span class="sxs-lookup"><span data-stu-id="ae46f-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="ae46f-183">응용 프로그램의 각 기능을 디자인 하는 경우는 어떻게 toomeasure는 성공을 사용자와 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="ae46f-184">시작, toorecord 필요 하 고 hello에서 앱에 이러한 이벤트에 대 한 호출을 추적 하는 hello를 코드로 비즈니스 이벤트를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="ae46f-185">A | B 테스트</span><span class="sxs-lookup"><span data-stu-id="ae46f-185">A | B Testing</span></span>
<span data-ttu-id="ae46f-186">어떤 유형의 기능 수 있습니다 알 수 없는 경우 각 toodifferent 액세스할 수 있는 사용자가 만드는 둘 모두에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="ae46f-187">또한 각각 hello 성공을 측정 하 고 tooa 통합 된 버전을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="ae46f-188">이 방법에 대 한 고유한 속성 값 tooall hello 원격 분석 응용 프로그램의 각 버전에서 전송 된 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="ae46f-189">Hello에서 속성을 정의 하 여 할 수 있습니다 활성 TelemetryContext 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="ae46f-190">이러한 기본 속성은 보내는 응용 프로그램 hello tooevery 원격 분석 메시지-사용자 사용자 지정 메시지 하지만 hello 표준 원격 분석 뿐만 아니라 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="ae46f-191">Hello Application Insights 포털에서 필터링 하 고 따라서 toocompare hello 서로 다른 버전으로 hello 속성 값에 데이터를 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="ae46f-192">toodo이 [원격 분석 이니셜라이저를 설정](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="ae46f-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="ae46f-193">Global.asax.cs 같은 웹 앱 이니셜라이저의 hello:</span><span class="sxs-lookup"><span data-stu-id="ae46f-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="ae46f-194">모든 새 TelemetryClients 지정한 hello 속성 값을 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="ae46f-195">개별 원격 분석 이벤트 hello 기본 값은 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae46f-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae46f-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae46f-196">Next steps</span></span>
   - [<span data-ttu-id="ae46f-197">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="ae46f-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="ae46f-198">깔때기</span><span class="sxs-lookup"><span data-stu-id="ae46f-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="ae46f-199">보존</span><span class="sxs-lookup"><span data-stu-id="ae46f-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="ae46f-200">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="ae46f-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="ae46f-201">통합 문서</span><span class="sxs-lookup"><span data-stu-id="ae46f-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="ae46f-202">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="ae46f-202">Add user context</span></span>](app-insights-usage-send-user-context.md)

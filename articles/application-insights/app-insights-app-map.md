---
title: "Azure Application Insights에서 맵 aaaApplication | Microsoft Docs"
description: "응용 프로그램 구성 요소 간의 hello 종속성의 시각적 표현을 레이블이 Kpi 및 경고와 함께 표시 됩니다."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="813b0-103">Application Insights의 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="813b0-103">Application Map in Application Insights</span></span>
<span data-ttu-id="813b0-104">[Azure Application Insights](app-insights-overview.md), 응용 프로그램 구조는 응용 프로그램 구성 요소의 hello 종속성 관계의 시각적 레이아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="813b0-105">각 구성 요소를 보여 줍니다 Kpi toohelp 부하, 성능, 오류 및 경고와 같은 성능 문제 또는 실패를 발생 시키는 구성 요소를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="813b0-106">모든 구성 요소 toomore에서 하나씩 클릭 하면 진단, 예: Application Insights 이벤트를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="813b0-107">앱에서 Azure 서비스를 사용 하는 경우 SQL 데이터베이스 관리자 권장 구성 같은 tooAzure 진단을 통해 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="813b0-108">다른 차트와 마찬가지로 응용 프로그램 맵 toohello가 올바르게 작동 하는 Azure 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="813b0-109">응용 프로그램 맵 열기 hello</span><span class="sxs-lookup"><span data-stu-id="813b0-109">Open hello application map</span></span>
<span data-ttu-id="813b0-110">응용 프로그램에 대 한 hello 개요 블레이드에서 맵 열기 hello:</span><span class="sxs-lookup"><span data-stu-id="813b0-110">Open hello map from hello overview blade for your application:</span></span>

![앱 맵 열기](./media/app-insights-app-map/01.png)

![앱 맵](./media/app-insights-app-map/02.png)

<span data-ttu-id="813b0-113">hello 맵은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-113">hello map shows:</span></span>

* <span data-ttu-id="813b0-114">가용성 테스트</span><span class="sxs-lookup"><span data-stu-id="813b0-114">Availability tests</span></span>
* <span data-ttu-id="813b0-115">클라이언트 측 구성 요소 (hello JavaScript SDK로 모니터링)</span><span class="sxs-lookup"><span data-stu-id="813b0-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="813b0-116">서버 쪽 구성 요소</span><span class="sxs-lookup"><span data-stu-id="813b0-116">Server-side component</span></span>
* <span data-ttu-id="813b0-117">Hello 클라이언트 및 서버 구성의 종속성</span><span class="sxs-lookup"><span data-stu-id="813b0-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="813b0-118">종속성 링크 그룹을 확장하고 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-118">You can expand and collapse dependency link groups:</span></span>

![축소](./media/app-insights-app-map/03.png)

<span data-ttu-id="813b0-120">SQL, HTTP 등 한 종류의 종속성이 많은 경우 그룹화되어 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![그룹화된 종속성](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="813b0-122">문제 발견</span><span class="sxs-lookup"><span data-stu-id="813b0-122">Spot problems</span></span>
<span data-ttu-id="813b0-123">각 노드에 해당 구성 요소에 대 한 hello 부하, 성능 및 실패 속도 같은 관련 된 성능 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="813b0-124">경고 아이콘은 발생 가능한 문제를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="813b0-125">주황색 경고는 요청, 페이지 보기 또는 종속성 호출에서 오류가 발생했음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="813b0-126">빨간색 경고는 5% 이상의 실패율을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="813b0-127">이러한 임계값 tooadjust을 원하는 경우 옵션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-127">If you want tooadjust these thresholds, open Options.</span></span>

![오류 아이콘](./media/app-insights-app-map/04.png)

<span data-ttu-id="813b0-129">활성 경고도 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-129">Active alerts also show up:</span></span> 

![활성 경고](./media/app-insights-app-map/05.png)

<span data-ttu-id="813b0-131">SQL Azure를 사용하는 경우 성능을 향상시키는 방법에 대한 권장 사항이 있는 경우 나타나는 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure 권장 사항](./media/app-insights-app-map/06.png)

<span data-ttu-id="813b0-133">자세한 내용은 모든 아이콘 tooget를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-133">Click any icon tooget more details:</span></span>

![Azure 권장 사항](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="813b0-135">진단 클릭</span><span class="sxs-lookup"><span data-stu-id="813b0-135">Diagnostic click through</span></span>
<span data-ttu-id="813b0-136">각 hello 노드 hello 지도에 진단에 대 한 대상으로 지정 된 클릭 광고를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="813b0-137">hello 옵션 hello hello 노드 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-137">hello options vary depending on hello type of hello node.</span></span>

![서버 옵션](./media/app-insights-app-map/09.png)

<span data-ttu-id="813b0-139">Azure에서 호스트 되는 구성 요소에 대 한 hello 옵션에 대 한 직접 링크 toothem을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="813b0-140">필터 및 시간 범위</span><span class="sxs-lookup"><span data-stu-id="813b0-140">Filters and time range</span></span>
<span data-ttu-id="813b0-141">기본적으로 hello 맵 hello 시간 범위 선택에 사용할 수 있는 모든 hello 데이터를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="813b0-142">하지만 tooinclude만 특정 작업 이름 또는 종속성 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="813b0-143">작업 이름: 페이지 보기 및 서버 쪽 요청 형식을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="813b0-144">이 옵션을 사용 hello 지도 표시만 hello 선택 작업에 대 한 hello 서버/클라이언트 쪽 노드에서 KPI를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="813b0-145">이러한 특정 작업의 hello 컨텍스트에서 호출 hello 종속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="813b0-146">종속성 기본 이름: hello AJAX 브라우저 종속성과 서버 쪽 종속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="813b0-147">사용자 지정 종속성 원격 분석 hello TrackDependency API로 보고 하는 경우 또한 여기에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="813b0-148">Hello 맵에 종속성 tooshow hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="813b0-149">현재이 옵션을이 선택 hello 서버 쪽 요청 또는 hello 클라이언트 쪽 페이지 보기에는 필터링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![필터 설정](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="813b0-151">필터 저장</span><span class="sxs-lookup"><span data-stu-id="813b0-151">Save filters</span></span>
<span data-ttu-id="813b0-152">toosave hello 필터를 적용 한 pin hello 필터링 된 뷰는 [대시보드](app-insights-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Pin toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="813b0-154">오류 창</span><span class="sxs-lookup"><span data-stu-id="813b0-154">Error pane</span></span>
<span data-ttu-id="813b0-155">Hello 맵에서 노드를 클릭할 때 오류 창의 해당 노드에 대 한 오류 요약으로 hello 오른쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="813b0-156">먼저 오류는 작업 ID별로 그룹화된 후 문제 ID별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![오류 창](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="813b0-158">실패에서을 클릭 하면 해당 오류 toohello 가장 최근 인스턴스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="813b0-159">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="813b0-159">Resource health</span></span>
<span data-ttu-id="813b0-160">일부 리소스 유형에 대 한 리소스 상태 hello 위쪽 hello 오류 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="813b0-161">예를 들어 SQL 노드를 클릭 하면 표시 됩니다 hello 데이터베이스 상태 및 경고가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![리소스 상태](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="813b0-163">해당 리소스에 대 한 hello 리소스 이름 tooview 표준 개요 메트릭을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="813b0-164">종단 간 시스템 앱 맵</span><span class="sxs-lookup"><span data-stu-id="813b0-164">End-to-end system app maps</span></span>

<span data-ttu-id="813b0-165">*SDK 버전 2.3 이상 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="813b0-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="813b0-166">응용 프로그램에 몇 가지 구성 요소로 구성 하는 경우 예를 들어 백 엔드 서비스 또한 toohello 웹 앱-합니다 표시 지도 하나의 통합 된 앱에서 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![필터 설정](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="813b0-168">hello 응용 프로그램 맵 Application Insights SDK를 설치 하는 hello와 서버 간의 모든 HTTP 종속성 호출에 따라 서버 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="813b0-169">각 Application Insights 리소스 toocontain 하나의 서버를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="813b0-170">다중 역할 앱 맵(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="813b0-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="813b0-171">hello 미리 보기 다중 역할 응용 프로그램 맵 기능은 toouse hello 앱 지도 데이터 toohello 보내는 여러 서버와 같은 Application Insights 리소스 / 계측 키입니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="813b0-172">서버 hello 지도에 원격 분석 항목 hello cloud_RoleName 속성으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="813b0-173">설정 *다중 역할 응용 프로그램 맵* 너무*에* 에서 hello 미리 보기 블레이드에서 tooenable이이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="813b0-174">이 방법은 마이크로 서비스 응용 프로그램 또는 단일 Application Insights 리소스 내의 여러 서버 toocorrelate 이벤트를 원하는 다른 시나리오에서 권장 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813b0-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="813b0-175">비디오</span><span class="sxs-lookup"><span data-stu-id="813b0-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="813b0-176">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="813b0-176">Feedback</span></span>
<span data-ttu-id="813b0-177">Hello 포털 사용자 의견 옵션을 통해 피드백을 제공 하십시오.</span><span class="sxs-lookup"><span data-stu-id="813b0-177">Please provide feedback through hello portal feedback option.</span></span>

![MapLink-1 이미지](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="813b0-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="813b0-179">Next steps</span></span>

* [<span data-ttu-id="813b0-180">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="813b0-180">Azure portal</span></span>](https://portal.azure.com)

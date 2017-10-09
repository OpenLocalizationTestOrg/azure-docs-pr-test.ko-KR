---
title: "OMS 로그 분석에서 aaaLog 검색 | Microsoft Docs"
description: "로그 검색 tooretrieve 로그 분석에서 모든 데이터가 필요합니다.  이 문서는 검색 로그 분석에 사용 되는 새로운 로그에 설명 하 고 하나를 만들기 전에 toounderstand 해야 하는 개념을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a><span data-ttu-id="0592e-104">Log Analytics의 로그 검색 이해</span><span class="sxs-lookup"><span data-stu-id="0592e-104">Understanding log searches in Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="0592e-105">이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 로그 검색을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-105">This article describes log searches in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="0592e-106">Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="0592e-107">작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="0592e-108">로그 검색 tooretrieve 로그 분석에서 모든 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-108">You require a log search tooretrieve any data from Log Analytics.</span></span>  <span data-ttu-id="0592e-109">Hello 포털에서 데이터를 분석 하 고 있는지 여부를 경고 규칙 toobe 구성에 대 한 알림을 특정 조건 또는 hello 로그 분석 API를 사용 하 여 데이터를 검색할 원하는 로그 검색 toospecify hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-109">Whether you're analyzing data in hello portal, configuring an alert rule toobe notified of a particular condition, or retrieving data using hello Log Analytics API, you will use a log search toospecify hello data you want.</span></span>  <span data-ttu-id="0592e-110">이 문서는 Log Analytics에서 로그 검색이 어떻게 사용되는지를 설명하고 새로 만들기 전에 이해해야 하는 개념을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-110">This article describes how log searches are used in Log Analytics and provides concepts that should understand before creating one.</span></span> <span data-ttu-id="0592e-111">Hello 참조 [다음 단계](#next-steps) hello 쿼리 언어에 대 한 자료 및 만들기 및 편집 로그 검색에 대 한 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="0592e-111">See hello [Next steps](#next-steps) section for details on creating and editing log searches and for references on hello query language.</span></span>

## <a name="where-log-searches-are-used"></a><span data-ttu-id="0592e-112">로그 검색이 사용되는 위치</span><span class="sxs-lookup"><span data-stu-id="0592e-112">Where log searches are used</span></span>

<span data-ttu-id="0592e-113">로그 검색을 사용 하는 로그 분석에는 hello 다양 한 방법 hello 다음 포함:</span><span class="sxs-lookup"><span data-stu-id="0592e-113">hello different ways that you will use log searches in Log Analytics include hello following:</span></span>

- <span data-ttu-id="0592e-114">**포털.**</span><span class="sxs-lookup"><span data-stu-id="0592e-114">**Portals.**</span></span> <span data-ttu-id="0592e-115">Hello로 hello 리포지토리에 데이터를 대화형으로 분석을 수행할 수 있습니다 [로그 검색 포털](log-analytics-log-search-log-search-portal.md) 또는 hello [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-115">You can perform interactive analysis of data in hello repository with hello [Log Search portal](log-analytics-log-search-log-search-portal.md) or hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="0592e-116">이렇게 하면 tooedit 프로그램 쿼리 및 다양 한 형식 및 시각화에에서 hello 결과 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-116">This allows you tooedit your query and analyze hello results in a variety of formats and visualizations.</span></span>  <span data-ttu-id="0592e-117">대부분의 쿼리를 만들면가 hello 포털 중 하나에서 시작 되 고 예상 대로 작동 하는지 확인 한 후 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-117">Most queries that you create will start in one of hello portals and then copied once you verify that it works as expected.</span></span>
- <span data-ttu-id="0592e-118">**경고 규칙.**</span><span class="sxs-lookup"><span data-stu-id="0592e-118">**Alert rules.**</span></span> <span data-ttu-id="0592e-119">[경고 규칙](log-analytics-alerts.md)은 작업 영역에서 데이터의 문제를 사전에 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-119">[Alert rules](log-analytics-alerts.md) proactively identify issues from data in your workspace.</span></span>  <span data-ttu-id="0592e-120">각 경고 규칙은 일정한 간격으로 자동으로 실행되는 로그 검색을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-120">Each alert rule is based on a log search that is automatically run at regular intervals.</span></span>  <span data-ttu-id="0592e-121">hello 결과가 경고를 생성 하면 검사 toodetermine 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-121">hello results are inspected toodetermine if an alert should be created.</span></span>
- <span data-ttu-id="0592e-122">**뷰.**</span><span class="sxs-lookup"><span data-stu-id="0592e-122">**Views.**</span></span>  <span data-ttu-id="0592e-123">사용자 대시보드 (포함)에 포함 된 데이터 toobe의 시각화를 만들 수 있습니다 [뷰 디자이너](log-analytics-view-designer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-123">You can create visualizations of data toobe included in user dashboards with [View Designer](log-analytics-view-designer.md).</span></span>  <span data-ttu-id="0592e-124">로그 검색에서 사용 하는 hello 데이터를 제공 [타일](log-analytics-view-designer-tiles.md) 및 [시각화 부분](log-analytics-view-designer-parts.md) 각 보기에서.</span><span class="sxs-lookup"><span data-stu-id="0592e-124">Log searches provide hello data used by [tiles](log-analytics-view-designer-tiles.md) and [visualization parts](log-analytics-view-designer-parts.md) in each view.</span></span>  <span data-ttu-id="0592e-125">Hello hello 데이터에 포털 tooperform 추가 분석 로그 검색으로 시각화 부분에서 다운 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-125">You can drill down from visualization parts into hello Log Search portal tooperform further analysis on hello data.</span></span>
- <span data-ttu-id="0592e-126">**내보내기.**</span><span class="sxs-lookup"><span data-stu-id="0592e-126">**Export.**</span></span>  <span data-ttu-id="0592e-127">로그 분석 작업 영역 tooExcel hello에서에서 데이터를 내보낼 때 또는 [Power BI](log-analytics-powerbi.md), 로그 검색 toodefine hello 데이터 tooexport를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-127">When you export data from hello Log Analytics workspace tooExcel or [Power BI](log-analytics-powerbi.md), you create a log search toodefine hello data tooexport.</span></span>
- <span data-ttu-id="0592e-128">**PowerShell.**</span><span class="sxs-lookup"><span data-stu-id="0592e-128">**PowerShell.**</span></span> <span data-ttu-id="0592e-129">명령줄 또는 사용 하는 Azure 자동화 runbook에서 PowerShell 스크립트를 실행할 수 있습니다 [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) 로그 분석에서 tooretrieve 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-129">You can run a PowerShell script from a command line or an Azure Automation runbook that uses [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve data from Log Analytics.</span></span>  <span data-ttu-id="0592e-130">이 cmdlet에는 쿼리 toodetermine hello 데이터 tooretrieve가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-130">This cmdlet requires a query toodetermine hello data tooretrieve.</span></span>
- <span data-ttu-id="0592e-131">**Log Analytics API.**</span><span class="sxs-lookup"><span data-stu-id="0592e-131">**Log Analytics API.**</span></span>  <span data-ttu-id="0592e-132">hello [로그 분석 로그 검색 API](log-analytics-log-search-api.md) 모든 REST API 클라이언트 hello 작업 영역에서 tooretrieve 데이터를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-132">hello [Log Analytics log search API](log-analytics-log-search-api.md) allows any REST API client tooretrieve data from hello workspace.</span></span>  <span data-ttu-id="0592e-133">로그 분석 toodetermine hello 데이터 tooretrieve에 대해 실행 되는 쿼리를 포함 하는 hello API 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-133">hello API request includes a query that is run against Log Analytics toodetermine hello data tooretrieve.</span></span>

![로그 검색](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a><span data-ttu-id="0592e-135">Log Analytics 데이터 구성 방법</span><span class="sxs-lookup"><span data-stu-id="0592e-135">How Log Analytics data is organized</span></span>
<span data-ttu-id="0592e-136">쿼리를 작성할 때 테이블 hello 하는 데이터를 찾고 확인 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-136">When you build a query, you start by determining which tables have hello data that you're looking for.</span></span> <span data-ttu-id="0592e-137">각 [데이터 소스](log-analytics-data-sources.md) 및 [솔루션](../operations-management-suite/operations-management-suite-solutions.md) hello 로그 분석 작업 영역에서 전용된 테이블에 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-137">Each [data source](log-analytics-data-sources.md) and [solution](../operations-management-suite/operations-management-suite-solutions.md) stores its data in dedicated tables in hello Log Analytics workspace.</span></span>  <span data-ttu-id="0592e-138">각 데이터 원본 및 솔루션에 대 한 설명서는 생성 된 hello 데이터 형식의 hello 이름 및 각 속성에 대 한 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-138">Documentation for each data source and solution includes hello name of hello data type that it creates and a description of each of its properties.</span></span>     <span data-ttu-id="0592e-139">많은 쿼리 되 면 필요 단일 테이블의 데이터를에서 하지만 다른 사용자 다양 한 옵션 tooinclude 여러 테이블의에서 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-139">Many queries will only require data from a single tables, but others may use a variety of options tooinclude data from multiple tables.</span></span>

![테이블](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a><span data-ttu-id="0592e-141">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="0592e-141">Writing a query</span></span>
<span data-ttu-id="0592e-142">로그의 hello 핵심 로그 분석에서 검색은 [광범위 한 쿼리 언어](https://docs.loganalytics.io/) 수 있게 해 주는 여러 가지 방법으로 hello 저장소에서 데이터를 분석 하 고 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-142">At hello core of log searches in Log Analytics is [an extensive query language](https://docs.loganalytics.io/) that lets you retrieve and analyze data from hello repository in a variety of ways.</span></span>  <span data-ttu-id="0592e-143">이 동일한 쿼리 언어는 [Application Insights](../application-insights/app-insights-analytics.md)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-143">This same query language is used for [Application Insights](../application-insights/app-insights-analytics.md).</span></span>  <span data-ttu-id="0592e-144">Toowrite 쿼리 로그 분석에서 중요 한 toocreating 로그 검색은 어떻게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-144">Learning how toowrite a query is critical toocreating log searches in Log Analytics.</span></span>  <span data-ttu-id="0592e-145">일반적으로 처음부터 기본 쿼리 및 다음 진행 toouse 더 높은 수준의 함수 요구 사항 복잡 해지면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-145">You'll typically start with basic queries and then progress toouse more advanced functions as your requirements become more complex.</span></span>

<span data-ttu-id="0592e-146">쿼리의 hello 기본 구조는 일련의 연산자 파이프 문자 뒤의 원본 테이블 `|`합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-146">hello basic structure of a query is a source table followed by a series of operators separated by a pipe character `|`.</span></span>  <span data-ttu-id="0592e-147">여러 연산자 toorefine hello 데이터를 함께 연결할 수 있으며 고급 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-147">You can chain together multiple operators toorefine hello data and perform advanced functions.</span></span>

<span data-ttu-id="0592e-148">예를 들어 한다고 가정 toofind hello 상위 10 개 컴퓨터가 hello로 대부분의 오류 이벤트 hello를 통해 어제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-148">For example, suppose you wanted toofind hello top ten computers with hello most error events over hello past day.</span></span>

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

<span data-ttu-id="0592e-149">또는 hello 마지막 날에에서 하트 비트를 보유 한 하지 않은 toofind 컴퓨터 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-149">Or maybe you want toofind computers that haven't had a heartbeat in hello last day.</span></span>

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

<span data-ttu-id="0592e-150">어떻습니까와 꺾은선형 차트는 각 컴퓨터에서 지난 주에 대 한 hello 프로세서 사용률?</span><span class="sxs-lookup"><span data-stu-id="0592e-150">How about a line chart with hello processor utilization for each computer from last week?</span></span>

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

<span data-ttu-id="0592e-151">Hello 쿼리의 구조는와 작업 하는 데이터의 hello 종류에 관계 없이 hello는 이러한 빠른 예제에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-151">You can see from these quick samples that regardless of hello kind of data that you're working with, hello structure of hello query is similar.</span></span>  <span data-ttu-id="0592e-152">Hello 파이프라인 toohello 다음 명령을 통해 hello 명령 하나에서 결과 데이터를 보내는 위치 고유 단계로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-152">You can break it down into distinct steps where hello resulting data from one command is sent through hello pipeline toohello next command.</span></span>

<span data-ttu-id="0592e-153">자습서 및 언어 참조를 포함 하 여 hello Azure 로그 분석 쿼리 언어에 대 한 전체 설명서를 참조 hello [Azure 로그 분석 쿼리 언어 설명서](https://docs.loganalytics.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-153">For complete documentation on hello Azure Log Analytics query language including tutorials and language reference, see hello [Azure Log Analytics query language documentation](https://docs.loganalytics.io/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0592e-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0592e-154">Next steps</span></span>

- <span data-ttu-id="0592e-155">Hello에 대 한 자세한 내용은 [toocreate를 사용 하 고 로그 검색을 편집 하는 포털](log-analytics-log-search-portals.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-155">Learn about hello [portals that you use toocreate and edit log searches](log-analytics-log-search-portals.md).</span></span>
- <span data-ttu-id="0592e-156">체크 아웃 한 [쿼리 작성의 자습서](https://go.microsoft.com/fwlink/?linkid=856078) hello 새로운 쿼리 언어를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0592e-156">Check out a [tutorial on writing queries](https://go.microsoft.com/fwlink/?linkid=856078) using hello new query language.</span></span>

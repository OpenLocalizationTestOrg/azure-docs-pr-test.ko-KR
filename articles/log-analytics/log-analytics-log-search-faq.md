---
title: "Log Analytics 새 로그 검색 질문과 대답 | Microsoft 문서"
description: "이 문서에서는 Log Analytics를 새 쿼리 언어로 업그레이드하는 과정과 관련된 질문과 대답을 제공합니다."
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
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: d7bd0d780c265cc15ad09a73ede8c5a886005e37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a><span data-ttu-id="27547-103">Log Analytics 새 로그 검색 FAQ 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="27547-103">Log Analytics new log search FAQ and known issues</span></span>

<span data-ttu-id="27547-104">이 문서에는 [새 쿼리 언어로의 Log Analytics](log-analytics-log-search-upgrade.md) 업그레이드와 관련한 질문과 대답 및 알려진 문제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-104">This article includes frequently asked questions and known issues regarding the upgrade of [Log Analytics to the new query language](log-analytics-log-search-upgrade.md).</span></span>  <span data-ttu-id="27547-105">작업 영역을 업그레이드하도록 결정하기 전에 이 전체 문서를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-105">You should read through this entire article before making the decision to upgrade your workspace.</span></span>


## <a name="alerts"></a><span data-ttu-id="27547-106">경고</span><span class="sxs-lookup"><span data-stu-id="27547-106">Alerts</span></span>

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-to-create-them-again-in-the-new-language-after-i-upgrade"></a><span data-ttu-id="27547-107">질문: 경고 규칙이 매우 많습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-107">Question: I have a lot of alert rules.</span></span> <span data-ttu-id="27547-108">업그레이드 후에 새 언어로 규칙을 다시 만들어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="27547-108">Do I need to create them again in the new language after I upgrade?</span></span>  
<span data-ttu-id="27547-109">아니요, 경고 규칙은 업그레이드 중에 새 검색 언어로 자동 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-109">No, your alert rules are automatically converted to the new search language during upgrade.</span></span>  


## <a name="computer-groups"></a><span data-ttu-id="27547-110">컴퓨터 그룹</span><span class="sxs-lookup"><span data-stu-id="27547-110">Computer groups</span></span>

### <a name="question-im-getting-errors-when-trying-to-use-computer-groups--has-their-syntax-changed"></a><span data-ttu-id="27547-111">질문: 컴퓨터 그룹을 사용하려고 할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-111">Question: I'm getting errors when trying to use computer groups.</span></span>  <span data-ttu-id="27547-112">구문이 변경되었나요?</span><span class="sxs-lookup"><span data-stu-id="27547-112">Has their syntax changed?</span></span>
<span data-ttu-id="27547-113">예, 작업 영역이 업그레이드될 때 컴퓨터 그룹을 사용하는 구문이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-113">Yes, the syntax for using computer groups changes when your workspace is upgraded.</span></span>  <span data-ttu-id="27547-114">자세한 내용은 [Log Analytics 로그 검색의 컴퓨터 그룹](log-analytics-computer-groups.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27547-114">See [Computer groups in Log Analytics log searches](log-analytics-computer-groups.md) for details.</span></span>

### <a name="known-issue-groups-imported-from-active-directory"></a><span data-ttu-id="27547-115">알려진 문제: Active Directory에서 가져온 그룹</span><span class="sxs-lookup"><span data-stu-id="27547-115">Known issue: Groups imported from Active Directory</span></span>
<span data-ttu-id="27547-116">현재 Active Directory에서 가져온 컴퓨터 그룹을 사용하는 쿼리를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-116">You cannot currently create a query that uses a computer group imported from Active Directory.</span></span>  <span data-ttu-id="27547-117">해결 방법으로, 이 문제를 해결할 때까지 가져온 Active Directory 그룹을 사용하여 새 컴퓨터 그룹 만든 다음, 쿼리에 해당 새 그룹을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-117">As a workaround until this issue is corrected, create a new computer group using the imported Active Directory group and then use that new group in your query.</span></span>

<span data-ttu-id="27547-118">가져온 Active Directory 그룹을 포함하는 새 컴퓨터 그룹을 만드는 쿼리의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-118">An example query to create a new computer group that includes an imported Active Directory group is as follows:</span></span>

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a><span data-ttu-id="27547-119">대시보드</span><span class="sxs-lookup"><span data-stu-id="27547-119">Dashboards</span></span>

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a><span data-ttu-id="27547-120">질문: 대시보드를 업그레이드된 작업 영역에서 계속 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="27547-120">Question: Can I still use dashboards in an upgraded workspace?</span></span>
<span data-ttu-id="27547-121">작업 영역을 업그레이드하기 전에 추가한 **내 대시보드**를 계속 사용할 수 있습니다. 하지만 해당 타일을 편집하거나 새로 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-121">You can continue to use any tiles that you added to **My Dashboard** before your workspace was upgraded, but you cannot edit those tiles or add new ones.</span></span>  <span data-ttu-id="27547-122">[뷰 디자이너](log-analytics-view-designer.md)로 뷰를 계속 만들고 편집할 수 있으며, Azure Portal에서 대시보드를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-122">You can continue to create and edit views with [View Designer](log-analytics-view-designer.md) and also create dashboards in the Azure portal.</span></span>


## <a name="log-searches"></a><span data-ttu-id="27547-123">로그 검색</span><span class="sxs-lookup"><span data-stu-id="27547-123">Log searches</span></span>

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-to-the-new-search-language-automatically"></a><span data-ttu-id="27547-124">질문: 업그레이드한 작업 영역 외부에 저장된 검색이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-124">Question: I have saved searches outside of my upgraded workspace.</span></span> <span data-ttu-id="27547-125">이러한 검색을 새 검색 언어로 자동 변환할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="27547-125">Can I convert them to the new search language automatically?</span></span>
<span data-ttu-id="27547-126">로그 검색 페이지의 언어 변환기 도구를 사용하면 각 검색을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-126">You can use the language converter tool in the log search page to convert each one.</span></span>  <span data-ttu-id="27547-127">작업 영역을 업그레이드하지 않고 여러 검색을 자동으로 변환하는 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-127">There is no method to automatically convert multiple searches without upgrading the workspace.</span></span>

### <a name="question-why-are-my-query-results-not-sorted"></a><span data-ttu-id="27547-128">질문: 내 쿼리 결과가 정렬되지 않는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="27547-128">Question: Why are my query results not sorted?</span></span>
<span data-ttu-id="27547-129">새 쿼리 언어에서는 결과가 기본적으로 정렬되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-129">Results are not sorted by default in the new query language.</span></span>  <span data-ttu-id="27547-130">[정렬 연산자](https://go.microsoft.com/fwlink/?linkid=856079)를 사용하여 하나 이상의 속성으로 결과를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-130">Use the [sort operator](https://go.microsoft.com/fwlink/?linkid=856079) to sort your results by one or more properties.</span></span>

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a><span data-ttu-id="27547-131">알려진 문제: 목록의 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="27547-131">Known issue: Search results in a list may include properties with no data</span></span>
<span data-ttu-id="27547-132">목록의 로그 검색 결과에 데이터가 없는 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-132">Log search results in a list may display properties with no data.</span></span>  <span data-ttu-id="27547-133">업그레이드하기 전에 이러한 속성을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-133">Prior to upgrade, these properties wouldn't be included.</span></span>  <span data-ttu-id="27547-134">이 문제는 빈 속성은 표시되지 않도록 수정될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-134">This issue will be corrected so that empty properties are not displayed.</span></span>

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a><span data-ttu-id="27547-135">알려진 문제: 차트에서 값을 선택하면 자세한 결과가 표시되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="27547-135">Known issue: Selecting a value in a chart doesn't display detailed results</span></span>
<span data-ttu-id="27547-136">업그레이드하기 전에 차트에서 값을 선택하면 선택한 값과 일치하는 레코드의 자세한 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-136">Prior to upgrade, when you selected a value in a chart, it would return a detailed list of records matching the selected value.</span></span>  <span data-ttu-id="27547-137">업그레이드 후에 단일 요약된 줄만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-137">After upgrade, only the single summarized line is returned.</span></span>  <span data-ttu-id="27547-138">이 문제는 현재 조사 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-138">This issue is currently being investigated.</span></span>

## <a name="log-search-api"></a><span data-ttu-id="27547-139">로그 검색 API</span><span class="sxs-lookup"><span data-stu-id="27547-139">Log Search API</span></span>

### <a name="question-does-the-log-search-api-get-updated-after-i-upgrade"></a><span data-ttu-id="27547-140">질문: 제가 업그레이드를 수행한 후에 로그 검색 API가 업데이트되었습니까?</span><span class="sxs-lookup"><span data-stu-id="27547-140">Question: Does the Log Search API get updated after I upgrade?</span></span>
<span data-ttu-id="27547-141">[로그 검색 API](log-analytics-log-search-api.md)는 아직 새 검색 언어로 업그레이드되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-141">The [Log Search API](log-analytics-log-search-api.md) has not yet been upgraded to the new search language.</span></span>  <span data-ttu-id="27547-142">작업 영역을 업그레이드한 후에도 이 API로 레거시 쿼리 언어를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-142">Continue to use the legacy query language with this API, even after you upgrade your workspace.</span></span>  <span data-ttu-id="27547-143">로그 검색 API가 업데이트되면 업데이트된 해당 설명서를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-143">Updated documentation will become available for the Log Search API when it's updated.</span></span>


## <a name="portals"></a><span data-ttu-id="27547-144">포털</span><span class="sxs-lookup"><span data-stu-id="27547-144">Portals</span></span>

### <a name="question-should-i-use-the-new-advanced-analytics-portal-or-keep-using-the-log-search-portal"></a><span data-ttu-id="27547-145">질문: 새 고급 분석 포털을 사용해야 합니까? 아니면 로그 검색 포털을 계속 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="27547-145">Question: Should I use the new Advanced Analytics portal or keep using the Log Search portal?</span></span>
<span data-ttu-id="27547-146">[Azure Log Analytics에서 로그 쿼리를 만들고 편집하기 위한 포털](log-analytics-log-search-portals.md)에서 두 포털의 비교를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-146">You can see a comparison of the two portals at [Portals for creating and editing log queries in Azure Log Analytics](log-analytics-log-search-portals.md).</span></span>  <span data-ttu-id="27547-147">각 포털은 분명한 이점이 있으므로 자신의 요구 사항에 가장 적합한 포털을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-147">Each has distinct advantages so you can choose the best one for your requirements.</span></span>  <span data-ttu-id="27547-148">두 포털 모두 고급 분석 포털에서 쿼리를 작성하고 뷰 디자이너와 같은 다른 위치에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-148">It's common to write queries in the Advanced Analytics portal and paste them into other places such as View Designer.</span></span>  <span data-ttu-id="27547-149">이를 수행할 때 [고려해야 할 문제](log-analytics-log-search-portals.md#advanced-analytics-portal)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="27547-149">You should read about [issues to consider](log-analytics-log-search-portals.md#advanced-analytics-portal) when doing that.</span></span>


## <a name="power-bi"></a><span data-ttu-id="27547-150">Power BI</span><span class="sxs-lookup"><span data-stu-id="27547-150">Power BI</span></span>

### <a name="question-does-anything-change-with-powerbi-integration"></a><span data-ttu-id="27547-151">질문: PowerBI 통합에서 변경되는 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="27547-151">Question: Does anything change with PowerBI integration?</span></span>
<span data-ttu-id="27547-152">예.</span><span class="sxs-lookup"><span data-stu-id="27547-152">Yes.</span></span>  <span data-ttu-id="27547-153">작업 영역이 업그레이드되면 Log Analytics 데이터를 Power BI로 내보내는 프로세스가 더 이상 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-153">Once your workspace has been upgraded then the process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="27547-154">그러면 업그레이드 전에 만든 모든 기존 일정을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-154">Any existing schedules that you created before upgrading will become disabled.</span></span>  <span data-ttu-id="27547-155">업그레이드 후 Azure Log Analytics는 Application Insights와 같은 플랫폼을 사용하며, [Application Insights 쿼리를 Power BI로 내보내는 프로세스](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)와 같은 프로세스를 사용하여 Log Analytics 쿼리를 Power BI로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27547-155">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>

### <a name="known-issue-power-bi-request-size-limit"></a><span data-ttu-id="27547-156">알려진 문제: Power BI 요청 크기 제한</span><span class="sxs-lookup"><span data-stu-id="27547-156">Known issue: Power BI request size limit</span></span>
<span data-ttu-id="27547-157">현재 Power BI로 내보낼 수 있는 Log Analytics 쿼리에 대한 크기 제한은 8MB입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-157">There is currently a size limit of 8 MB for a Log Analytics query that can be exported to Power BI.</span></span>  <span data-ttu-id="27547-158">이 한도는 나중에 상향 조정될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-158">This limit will be increased soon.</span></span>


##<a name="powershell-cmdlets"></a><span data-ttu-id="27547-159">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="27547-159">PowerShell cmdlets</span></span>

### <a name="question-does-the-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a><span data-ttu-id="27547-160">질문: 제가 업그레이드를 수행한 후에 로그 검색 PowerShell cmdlet이 업데이트되었습니까?</span><span class="sxs-lookup"><span data-stu-id="27547-160">Question: Does the Log Search PowerShell cmdlet get updated after I upgrade?</span></span>
<span data-ttu-id="27547-161">[Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults)는 새 검색 언어로 아직 업그레이드되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-161">The [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) has not yet been upgraded to the new search language.</span></span>  <span data-ttu-id="27547-162">작업 영역을 업그레이드한 후에도 이 cmdlet으로 레거시 쿼리 언어를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-162">Continue to use the legacy query language with this cmdlet, even after you upgrade your workspace.</span></span>  <span data-ttu-id="27547-163">cmdlet이 업데이트되면 업데이트된 해당 설명서를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-163">Updated documentation will become available for the cmdlet when it's updated.</span></span>


## <a name="resource-manager-templates"></a><span data-ttu-id="27547-164">리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="27547-164">Resource Manager templates</span></span>

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a><span data-ttu-id="27547-165">질문: Resource Manager 템플릿을 사용하여 업그레이드된 작업 영역을 작성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="27547-165">Question: Can I create an upgraded workspace with a Resource Manager template?</span></span>
<span data-ttu-id="27547-166">예.</span><span class="sxs-lookup"><span data-stu-id="27547-166">Yes.</span></span>  <span data-ttu-id="27547-167">2017년 3월 15일 미리 보기의 API 버전을 사용하고 다음 예제와 같이 템플릿의 **기능** 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-167">You must use an API version of 2017-03-15-preview and include a **features** section in your template as in the following example.</span></span>

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a><span data-ttu-id="27547-168">솔루션</span><span class="sxs-lookup"><span data-stu-id="27547-168">Solutions</span></span>

### <a name="question-will-my-solutions-continue-to-work"></a><span data-ttu-id="27547-169">질문: 내 솔루션이 계속 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="27547-169">Question: Will my solutions continue to work?</span></span>
<span data-ttu-id="27547-170">모든 솔루션은 업그레이드된 작업 영역에서 계속 작동합니다. 단, 새 쿼리 언어로 변환된 경우 성능은 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-170">All solutions will continue to work in an upgraded workspace, although their performance will improve if they are converted to the new query language.</span></span>  <span data-ttu-id="27547-171">이 섹션에 설명된 일부 기존 솔루션에는 알려진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-171">There are known issues with some existing solutions that are described in this section.</span></span>

### <a name="known-issue-capacity-and-performance-solution"></a><span data-ttu-id="27547-172">알려진 문제: 용량 및 성능 솔루션</span><span class="sxs-lookup"><span data-stu-id="27547-172">Known issue: Capacity and Performance solution</span></span>
<span data-ttu-id="27547-173">[용량 및 성능](log-analytics-capacity.md) 보기의 일부는 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-173">Some of the parts in the [Capacity and Performance](log-analytics-capacity.md) view may be empty.</span></span>  <span data-ttu-id="27547-174">이 문제에 대한 수정은 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-174">A fix to this issue will be available shortly.</span></span>

### <a name="known-issue-device-health-solution"></a><span data-ttu-id="27547-175">알려진 문제: 장치 상태 솔루션</span><span class="sxs-lookup"><span data-stu-id="27547-175">Known issue: Device Health solution</span></span>
<span data-ttu-id="27547-176">[장치 상태 솔루션](https://docs.microsoft.com/windows/deployment/update/device-health-monitor)은 업그레이드된 작업 영역의 데이터를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-176">The [Device Health solution](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) will not collect data in an upgraded workspace.</span></span>  <span data-ttu-id="27547-177">이 문제에 대한 수정은 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-177">A fix to this issue will be available shortly.</span></span>

### <a name="known-issue-application-insights-connector"></a><span data-ttu-id="27547-178">알려진 문제: Application Insights 커넥터</span><span class="sxs-lookup"><span data-stu-id="27547-178">Known issue: Application Insights connector</span></span>
<span data-ttu-id="27547-179">[Application Insights 커넥터 솔루션](log-analytics-app-insights-connector.md)의 관점은 현재 업그레이드된 작업 영역에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-179">Perspectives in [Application Insights Connector solution](log-analytics-app-insights-connector.md) are currently not supported in an upgraded workspace.</span></span>  <span data-ttu-id="27547-180">이 문제에 대한 수정은 현재 분석 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-180">A fix to this issue is currently under analysis.</span></span>

## <a name="upgrade-process"></a><span data-ttu-id="27547-181">업그레이드 프로세스</span><span class="sxs-lookup"><span data-stu-id="27547-181">Upgrade process</span></span>

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-the-same-time"></a><span data-ttu-id="27547-182">질문: 작업 영역이 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-182">Question: I have several workspaces.</span></span> <span data-ttu-id="27547-183">모든 작업 영역을 동시에 업그레이드할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="27547-183">Can I upgrade all workspaces at the same time?</span></span>  
<span data-ttu-id="27547-184">아니요.</span><span class="sxs-lookup"><span data-stu-id="27547-184">No.</span></span>  <span data-ttu-id="27547-185">각 업그레이드는 단일 작업 영역에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-185">Upgrade applies to a single workspace each time.</span></span> <span data-ttu-id="27547-186">현재는 여러 작업 영역을 한 번에 업그레이드할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-186">Currently there is no way of upgrading many workspaces at once.</span></span> <span data-ttu-id="27547-187">업그레이드된 작업 영역의 다른 사용자도 영향을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-187">Please note that other users of the upgraded workspace will be affected as well.</span></span>  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a><span data-ttu-id="27547-188">질문: 업그레이드하면 작업 영역에 수집되어 있는 기존 로그 데이터가 수정되나요?</span><span class="sxs-lookup"><span data-stu-id="27547-188">Question: Will existing log data collected in my workspace be modified if I upgrade?</span></span>  
<span data-ttu-id="27547-189">아니요.</span><span class="sxs-lookup"><span data-stu-id="27547-189">No.</span></span> <span data-ttu-id="27547-190">작업 영역 검색에 사용할 수 있는 로그 데이터는 업그레이드의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-190">The log data available to your workspace searches is not affected by the upgrade.</span></span> <span data-ttu-id="27547-191">저장된 검색, 경고 및 보기는 새 검색 언어로 자동 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-191">Saved searches, alerts and views will be converted to the new search language automatically.</span></span>  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a><span data-ttu-id="27547-192">질문: 내 작업 영역을 업그레이드하지 않으면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="27547-192">Question: What happens if I don't upgrade my workspace?</span></span>  
<span data-ttu-id="27547-193">향후 몇 개월 이내에 레거시 로그 검색은 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-193">The legacy log search will be deprecated in the coming months.</span></span> <span data-ttu-id="27547-194">이 시점까지 업그레이드하지 않은 작업 영역은 자동으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-194">Workspaces that are not upgraded by that time will be upgraded automatically.</span></span>

### <a name="question-i-didnt-choose-to-upgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a><span data-ttu-id="27547-195">질문: 업그레이드를 선택하지 않았는데도 내 작업 영역이 업그레이드되었습니다!</span><span class="sxs-lookup"><span data-stu-id="27547-195">Question: I didn't choose to upgrade, but my workspace has been upgraded anyway!</span></span> <span data-ttu-id="27547-196">어떻게 된 건가요?</span><span class="sxs-lookup"><span data-stu-id="27547-196">What happened?</span></span>  
<span data-ttu-id="27547-197">해당 작업 영역의 다른 관리자의 작업 영역을 업그레이드했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-197">Another admin of this workspace could have upgraded the workspace.</span></span> <span data-ttu-id="27547-198">새 언어가 일반 공급 상태가 되면 모든 작업 영역은 자동으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-198">Please note that all workspaces will be automatically upgraded when the new language reaches general availability.</span></span>  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-to-cancel-it-and-restore-everything-back-what-should-i-do"></a><span data-ttu-id="27547-199">질문: 실수로 업그레이드를 해서 취소하고 모든 항목을 다시 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27547-199">Question: I have upgraded by mistake and now need to cancel it and restore everything back.</span></span> <span data-ttu-id="27547-200">어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="27547-200">What should I do?!</span></span>  
<span data-ttu-id="27547-201">걱정하실 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-201">No problem.</span></span>  <span data-ttu-id="27547-202">업그레이드 전에 작업 영역의 스냅숏이 생성되었으므로 해당 스냅숏을 복원하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-202">We create a snapshot of your workspace before upgrade, so you can restore it.</span></span> <span data-ttu-id="27547-203">하지만 업그레이드 후에 저장한 검색, 경고 또는 보기는 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-203">Keep in mind that searches, alerts or views you saved after the upgrade will be lost though.</span></span>  <span data-ttu-id="27547-204">작업 영역 환경을 복원하려면 [업그레이드 후에 다시 원래대로 되돌릴 수 있나요?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)의 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="27547-204">To restore your workspace environment, follow the procedure at [Can I go back after I upgrade?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)</span></span>


## <a name="views"></a><span data-ttu-id="27547-205">뷰</span><span class="sxs-lookup"><span data-stu-id="27547-205">Views</span></span>

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a><span data-ttu-id="27547-206">질문: 뷰 디자이너를 통해 새 뷰를 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="27547-206">Question: How do I create a new view with View Designer?</span></span>
<span data-ttu-id="27547-207">업그레이드하기 전에 주 대시보드의 타일에서 뷰 디자이너로 새 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-207">Prior to upgrade, you could create a new view with View Designer from a tile on the main dashboard.</span></span>  <span data-ttu-id="27547-208">작업 영역이 업그레이드되면 이 타일은 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-208">When your workspace is upgraded, this tile is removed.</span></span>  <span data-ttu-id="27547-209">왼쪽 메뉴의 녹색 + 단추를 클릭하여 OMS 포털에서 뷰 디자이너로 새 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-209">You can create a new view with View Designer in the OMS portal by clicking on the green + button in the left menu.</span></span>

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a><span data-ttu-id="27547-210">알려진 문제: 뷰에서 꺾은선형 차트에 대한 모두 보기 옵션을 사용해도 꺾은선형 차트로 결과가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27547-210">Known issue: See all option for line charts in views doesn't result in a line chart</span></span>
<span data-ttu-id="27547-211">뷰의 꺾은선형 차트에서 아래쪽에 *모두 보기*옵션을 클릭하면 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-211">When you click on the *See all* option at the bottom of a line chart part in a view, you are presented with a table.</span></span>  <span data-ttu-id="27547-212">업그레이드하기 전에는 꺾은선형 차트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27547-212">Prior to upgrade, you would be presented with a line chart.</span></span>  <span data-ttu-id="27547-213">이 문제는 잠재적 수정에 대한 분석 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27547-213">This issue is being analyzed for a potential modification.</span></span>


## <a name="next-steps"></a><span data-ttu-id="27547-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27547-214">Next steps</span></span>

- <span data-ttu-id="27547-215">[새 Log Analytics 쿼리 언어로 작업 영역 업그레이드](log-analytics-log-search-upgrade.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27547-215">Learn more about [upgrading your workspace to the new Log Analytics query language](log-analytics-log-search-upgrade.md).</span></span>

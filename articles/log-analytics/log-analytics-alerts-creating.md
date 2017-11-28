---
title: "OMS Log Analytics에서 경고 만들기 | Microsoft Docs"
description: "Log Analytics의 경고는 OMS 저장소의 중요한 정보를 식별하며 문제를 미리 알리거나 작업을 호출하여 문제 해결을 시도합니다.  이 문서에서는 경고 규칙을 만드는 방법을 설명하고 규칙에서 실행할 수 있는 여러 가지 작업을 자세히 설명합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: c34fb7295e8f386f0e7cf2c1db6b26a3e49eae98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a><span data-ttu-id="13ed9-104">Log Analytics에서 경고 규칙 작업</span><span class="sxs-lookup"><span data-stu-id="13ed9-104">Working with alert rules in Log Analytics</span></span>
<span data-ttu-id="13ed9-105">경고는 일정한 간격으로 로그 검색을 자동으로 실행하는 경고 규칙에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-105">Alerts are created by alert rules that automatically run log searches at regular intervals.</span></span>  <span data-ttu-id="13ed9-106">결과가 특정 조건과 일치하는 경우 경고 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-106">They create an alert record if the results match particular criteria.</span></span>  <span data-ttu-id="13ed9-107">그런 다음 규칙에 따라 하나 이상의 작업이 자동으로 실행되어 경고를 미리 알리거나 다른 프로세스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-107">The rule can then automatically run one or more actions to proactively notify you of the alert or invoke another process.</span></span>   

<span data-ttu-id="13ed9-108">이 문서에서는 OMS 포털을 사용하여 경고 규칙을 만들고 편집하는 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-108">This article describes the processes to create and edit alert rules using the OMS portal.</span></span>  <span data-ttu-id="13ed9-109">다양한 설정 및 필요한 논리를 구현하는 방법에 대한 자세한 내용은 [Log Analytics의 경고 이해](log-analytics-alerts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13ed9-109">For details about the different settings and how to implement required logic, see [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

>[!NOTE]
> <span data-ttu-id="13ed9-110">현재 Azure Portal을 사용하여 경고 규칙을 만들거나 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-110">You cannot currently create or modify an alert rule using the Azure portal.</span></span> 

## <a name="create-an-alert-rule"></a><span data-ttu-id="13ed9-111">경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="13ed9-111">Create an alert rule</span></span>

<span data-ttu-id="13ed9-112">OMS 포털을 사용하여 경고 규칙을 만들려면 경고를 호출해야 하는 레코드에 대한 로그 검색을 만드는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-112">To create an alert rule using the OMS portal, you start by creating a log search for the records that should invoke the alert.</span></span>  <span data-ttu-id="13ed9-113">그러면 **경고** 단추를 사용할 수 있으며 이 단추를 사용하여 경고 규칙을 만들고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-113">The **Alert** button will then be available so you can create and configure the alert rule.</span></span>

>[!NOTE]
> <span data-ttu-id="13ed9-114">현재 OMS 작업 영역에서 최대 250개의 경고 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-114">A maximum of 250 alert rules can currently be created in an OMS workspace.</span></span> 

1. <span data-ttu-id="13ed9-115">OMS 개요 페이지에서 **로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-115">From the OMS Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="13ed9-116">새 로그 검색 쿼리를 만들거나 저장된 로그 검색을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-116">Either create a new log search query or select a saved log search.</span></span> 
3. <span data-ttu-id="13ed9-117">페이지 위쪽에서 **경고**를 클릭하여 **경고 규칙 추가** 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-117">Click **Alert** at the top of the page to open the **Add Alert Rule** screen.</span></span>
4. <span data-ttu-id="13ed9-118">아래 [경고 규칙의 세부 정보](#details-of-alert-rules)의 정보를 사용하여 경고 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-118">Configure the alert rule using information in [Details of alert rules](#details-of-alert-rules) below.</span></span>
6. <span data-ttu-id="13ed9-119">**저장** 을 클릭하여 경고 규칙을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-119">Click **Save** to complete the alert rule.</span></span>  <span data-ttu-id="13ed9-120">실행을 즉시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-120">It will start running immediately.</span></span>


## <a name="edit-an-alert-rule"></a><span data-ttu-id="13ed9-121">경고 규칙 편집</span><span class="sxs-lookup"><span data-stu-id="13ed9-121">Edit an alert rule</span></span>
<span data-ttu-id="13ed9-122">Log Analytics **설정**의 **경고** 메뉴에서 모든 경고 규칙의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-122">You can get a list of all alert rules in the **Alerts** menu in Log Analytics **Settings**.</span></span>  

![경고 관리](./media/log-analytics-alerts/configure.png)

1. <span data-ttu-id="13ed9-124">OMS 콘솔에서 **설정** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-124">In the OMS console select the **Settings** tile.</span></span>
2. <span data-ttu-id="13ed9-125">**경고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-125">Select **Alerts**.</span></span>

<span data-ttu-id="13ed9-126">이 뷰에서 여러 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-126">You can perform multiple actions from this view.</span></span>

* <span data-ttu-id="13ed9-127">옆에 있는 **끄기** 를 선택하여 규칙을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-127">Disable a rule by selecting **Off** next to it.</span></span>
* <span data-ttu-id="13ed9-128">옆에 있는 연필 아이콘을 클릭하여 경고 규칙을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-128">Edit an alert rule by clicking the pencil icon next to it.</span></span>
* <span data-ttu-id="13ed9-129">옆에 있는 **X** 아이콘을 클릭하여 경고 규칙을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-129">Remove an alert rule by clicking the **X** icon next to it.</span></span> 

## <a name="details-of-alert-rules"></a><span data-ttu-id="13ed9-130">경고 규칙의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="13ed9-130">Details of alert rules</span></span>
<span data-ttu-id="13ed9-131">OMS 포털에서 경고 규칙을 만들거나 편집할 때 **경고 규칙 추가** 또는 **경고 규칙 편집** 페이지로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-131">When you create or edit an alert rule in the OMS portal, you work with the **Add Alert Rule** or **Edit Alert Rule** page.</span></span>  <span data-ttu-id="13ed9-132">다음 표는 이 화면의 필드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-132">The following tables describe the fields in this screen.</span></span>

![경고 규칙](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a><span data-ttu-id="13ed9-134">경고 정보</span><span class="sxs-lookup"><span data-stu-id="13ed9-134">Alert information</span></span>
<span data-ttu-id="13ed9-135">이는 경고 규칙에 대한 기본 설정 및 생성한 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-135">These are basic settings for the alert rule and the alerts it creates.</span></span>

| <span data-ttu-id="13ed9-136">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-136">Property</span></span> | <span data-ttu-id="13ed9-137">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-137">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-138">이름</span><span class="sxs-lookup"><span data-stu-id="13ed9-138">Name</span></span> | <span data-ttu-id="13ed9-139">경고 규칙을 식별하는 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-139">Unique name to identify the alert rule.</span></span> <span data-ttu-id="13ed9-140">이 이름은 규칙에 의해 생성된 모든 경고에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-140">This name is included in any alerts created by the rule.</span></span>  |
| <span data-ttu-id="13ed9-141">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-141">Description</span></span> | <span data-ttu-id="13ed9-142">경고 규칙에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-142">Optional description of the alert rule.</span></span> |
| <span data-ttu-id="13ed9-143">심각도</span><span class="sxs-lookup"><span data-stu-id="13ed9-143">Severity</span></span> |<span data-ttu-id="13ed9-144">이 규칙에 의해 생성된 모든 경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-144">Severity of any alerts created by this rule.</span></span> |

### <a name="search-query-and-time-window"></a><span data-ttu-id="13ed9-145">검색 쿼리 및 기간</span><span class="sxs-lookup"><span data-stu-id="13ed9-145">Search query and time window</span></span>
<span data-ttu-id="13ed9-146">경고를 만들어야 하는지 결정하도록 평가되는 레코드를 반환하는 검색 쿼리 및 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-146">The search query and time window that return the records that are evaluated to determine if any alerts should be created.</span></span>

| <span data-ttu-id="13ed9-147">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-147">Property</span></span> | <span data-ttu-id="13ed9-148">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-148">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-149">검색 쿼리</span><span class="sxs-lookup"><span data-stu-id="13ed9-149">Search query</span></span> | <span data-ttu-id="13ed9-150">실행될 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-150">This is the query that will be run.</span></span>  <span data-ttu-id="13ed9-151">이 쿼리에서 반환된 레코드는 경고를 생성할지 여부를 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-151">The records returned by this query will be used to determine whether an alert is created.</span></span><br><br><span data-ttu-id="13ed9-152">**현재 검색 쿼리 사용** 을 선택하여 현재 쿼리를 사용하거나 목록에서 기존 저장된 검색을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-152">Select **Use current search query** to use the current query or select an existing saved search from the list.</span></span>  <span data-ttu-id="13ed9-153">쿼리 구문이 텍스트 상자에 제공되며 필요하면 텍스트 상자의 내용을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-153">The query syntax is provided in the text box where you can modify it if necessary.</span></span> |
| <span data-ttu-id="13ed9-154">기간</span><span class="sxs-lookup"><span data-stu-id="13ed9-154">Time window</span></span> |<span data-ttu-id="13ed9-155">쿼리에 대한 시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-155">Specifies the time range for the query.</span></span>  <span data-ttu-id="13ed9-156">쿼리에서는 현재 시간의 이 범위 내에서 생성된 레코드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-156">The query returns only records that were created within this range of  the current time.</span></span>  <span data-ttu-id="13ed9-157">이는 5 분에서 24 시간 사이의 임의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-157">This can be any value between 5 minutes and 24 hours.</span></span>  <span data-ttu-id="13ed9-158">이는 경고 빈도보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-158">It should be greater than or equal to the alert frequency.</span></span>  <br><br> <span data-ttu-id="13ed9-159">예를 들어 기간을 60 분으로 설정했는데 오후 1시 15분에 쿼리를 실행하면 오후 12시 15분부터 오후 1시 15분 사이의 레코드만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-159">For example, If the time window is set to 60 minutes, and the query is run at 1:15 PM, only records created between 12:15 PM and 1:15 PM will be returned.</span></span> |

<span data-ttu-id="13ed9-160">경고 규칙에 대한 기간을 제공하는 경우 해당 기간에 대한 검색 조건과 일치하는 기존 레코드 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-160">When you provide the time window for the alert rule, the number of existing records that match the search criteria for that time window will be displayed.</span></span>  <span data-ttu-id="13ed9-161">이 정보는 예상하는 결과 수를 제공할 빈도를 결정하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-161">This can help you determine the frequency that will give you the number of results that you expect.</span></span>

### <a name="schedule"></a><span data-ttu-id="13ed9-162">일정</span><span class="sxs-lookup"><span data-stu-id="13ed9-162">Schedule</span></span>
<span data-ttu-id="13ed9-163">검색 쿼리를 실행하는 빈도를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-163">Defines how often the search query is run.</span></span>

| <span data-ttu-id="13ed9-164">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-164">Property</span></span> | <span data-ttu-id="13ed9-165">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-165">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-166">경고 빈도</span><span class="sxs-lookup"><span data-stu-id="13ed9-166">Alert frequency</span></span> | <span data-ttu-id="13ed9-167">쿼리를 실행해야 하는 빈도를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-167">Specifies how often the query should be run.</span></span> <span data-ttu-id="13ed9-168">5 분에서 24 시간 사이의 임의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-168">Can be any value between 5 minutes and 24 hours.</span></span> <span data-ttu-id="13ed9-169">기간보다 작거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-169">Should be equal to or less than the time window.</span></span>  <span data-ttu-id="13ed9-170">값이 기간보다 큰 경우 레코드가 누락될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-170">If the value is greater than the time window, then you risk records being missed.</span></span><br><br><span data-ttu-id="13ed9-171">예를 들어 30분의 기간과 60분의 빈도를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-171">For example, consider a time window of 30 minutes and a frequency of 60 minutes.</span></span>  <span data-ttu-id="13ed9-172">쿼리가 1:00에 실행되면 오후 12:30 및 1:00 사이의 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-172">If the query is run at 1:00, it returns records between 12:30 and 1:00 PM.</span></span>  <span data-ttu-id="13ed9-173">1:30 및 2:00 사이의 레코드를 반환하게 된다면 다음으로 쿼리가 실행되는 시간은 2:00입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-173">The next time the query would run is 2:00 when it would return records between 1:30 and 2:00.</span></span>  <span data-ttu-id="13ed9-174">1:00 및 1:30 사이에 생성된 레코드는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-174">Any records created between 1:00 and 1:30 would never be evaluated.</span></span> |


### <a name="generate-alert-based-on"></a><span data-ttu-id="13ed9-175">경고 생성 조건</span><span class="sxs-lookup"><span data-stu-id="13ed9-175">Generate alert based on</span></span>
<span data-ttu-id="13ed9-176">검색 쿼리 결과에 대해 평가할 조건을 정의하여 경고를 만들어야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-176">Defines the criteria that will be evaluated against the results of the search query to determine if an alert should be created.</span></span>  <span data-ttu-id="13ed9-177">이러한 세부 정보는 선택하는 경고 규칙의 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-177">These details will be different depending on the type of alert rule that you select.</span></span>  <span data-ttu-id="13ed9-178">[Log Analytics의 경고 이해](log-analytics-alerts.md)에서 다양한 경고 규칙 유형에 대한 세부 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-178">You can get details for the different alert rule types from [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

| <span data-ttu-id="13ed9-179">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-179">Property</span></span> | <span data-ttu-id="13ed9-180">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-180">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-181">알림 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="13ed9-181">Suppress alerts</span></span> | <span data-ttu-id="13ed9-182">경고 규칙 표시 안 함 기능을 켜면 규칙에 대한 작업이 새 경고를 만든 후 정의된 기간 동안 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-182">When you turn on suppression for the alert rule, actions for the rule are disabled for a defined length of time after creating a new alert.</span></span> <span data-ttu-id="13ed9-183">규칙은 여전히 실행되고 있으며 조건을 만족하면 경고 레코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-183">The rule is still running and will create alert records if the criteria is met.</span></span> <span data-ttu-id="13ed9-184">이 기능을 사용하여 중복 작업을 실행하지 않고 문제를 해결할 시간 여유를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-184">This is to allow you time to correct the problem without running duplicate actions.</span></span> |

#### <a name="number-of-results-alert-rules"></a><span data-ttu-id="13ed9-185">결과 수 경고 규칙</span><span class="sxs-lookup"><span data-stu-id="13ed9-185">Number of results alert rules</span></span>

| <span data-ttu-id="13ed9-186">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-186">Property</span></span> | <span data-ttu-id="13ed9-187">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-187">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-188">결과의 수</span><span class="sxs-lookup"><span data-stu-id="13ed9-188">Number of results</span></span> |<span data-ttu-id="13ed9-189">쿼리에서 반환된 레코드의 수가 제공한 값**보다 큰** 또는 값**보다 작은** 경우 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-189">An alert is created if the number of records returned by the query is either **greater than** or **less than** the value you provide.</span></span>  |

#### <a name="metric-measurement-alert-rules"></a><span data-ttu-id="13ed9-190">미터법 경고 규칙</span><span class="sxs-lookup"><span data-stu-id="13ed9-190">Metric measurement alert rules</span></span>

| <span data-ttu-id="13ed9-191">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-191">Property</span></span> | <span data-ttu-id="13ed9-192">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-192">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-193">집계 값</span><span class="sxs-lookup"><span data-stu-id="13ed9-193">Aggregate value</span></span> | <span data-ttu-id="13ed9-194">결과의 각 집계 값이 위반으로 간주되기 위해 초과해야 하는 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-194">Threshold value that each aggregate value in the results must exceed to be considered a breach.</span></span> |
| <span data-ttu-id="13ed9-195">경고 트리거 조건</span><span class="sxs-lookup"><span data-stu-id="13ed9-195">Trigger alert based on</span></span> | <span data-ttu-id="13ed9-196">만들려는 경고를 만들기 위한 위반 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-196">The number of breaches for an alert to be created.</span></span>  <span data-ttu-id="13ed9-197">결과 집합에서 모든 위반의 조합에 대해 **총 위반**을 지정하거나 **연속 위반**을 지정하여 연속된 샘플에서 위반이 발생해야 한다고 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-197">You can specify **Total breaches** for any combination of breaches across the results set or **Consecutive breaches** to require that the breaches must occur in consecutive samples.</span></span> |

### <a name="actions"></a><span data-ttu-id="13ed9-198">작업</span><span class="sxs-lookup"><span data-stu-id="13ed9-198">Actions</span></span>
<span data-ttu-id="13ed9-199">경고 규칙은 임계값이 충족되는 경우 항상 [경고 레코드](#alert-records)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-199">Alert rules will always create an [alert record](#alert-records) when the threshold is met.</span></span>  <span data-ttu-id="13ed9-200">또한 전자 메일 보내기 또는 Runbook 시작과 같은 하나 이상의 응답을 실행하도록 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-200">You can also define one or more responses to be run such as sending an email or starting a runbook.</span></span>



#### <a name="email-actions"></a><span data-ttu-id="13ed9-201">전자 메일 작업</span><span class="sxs-lookup"><span data-stu-id="13ed9-201">Email actions</span></span>
<span data-ttu-id="13ed9-202">전자 메일 작업은 한 명 이상의 수신자에게 경고의 세부 정보가 포함된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-202">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>

| <span data-ttu-id="13ed9-203">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-203">Property</span></span> | <span data-ttu-id="13ed9-204">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-204">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-205">메일 알림</span><span class="sxs-lookup"><span data-stu-id="13ed9-205">Email notification</span></span> |<span data-ttu-id="13ed9-206">경고가 트리거될 때 전자 메일을 보내려면 **예** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-206">Specify **Yes** if you want an email to be sent when the alert is triggered.</span></span> |
| <span data-ttu-id="13ed9-207">제목</span><span class="sxs-lookup"><span data-stu-id="13ed9-207">Subject</span></span> |<span data-ttu-id="13ed9-208">전자 메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-208">Subject in the email.</span></span>  <span data-ttu-id="13ed9-209">메일의 본문을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-209">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="13ed9-210">받는 사람</span><span class="sxs-lookup"><span data-stu-id="13ed9-210">Recipients</span></span> |<span data-ttu-id="13ed9-211">모든 전자 메일 받는 사람의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-211">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="13ed9-212">둘 이상의 주소를 지정하는 경우 주소를 세미콜론(;)으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-212">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="13ed9-213">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="13ed9-213">Webhook actions</span></span>
<span data-ttu-id="13ed9-214">웹후크 작업을 사용하여 단일 HTTP POST 요청을 통해 외부 프로세스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-214">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>

| <span data-ttu-id="13ed9-215">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-215">Property</span></span> | <span data-ttu-id="13ed9-216">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-216">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-217">웹후크</span><span class="sxs-lookup"><span data-stu-id="13ed9-217">Webhook</span></span> |<span data-ttu-id="13ed9-218">경고가 트리거될 때 웹후크를 호출하려면 **예** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-218">Specify **Yes** if you want to call a webhook when the alert is triggered.</span></span> |
| <span data-ttu-id="13ed9-219">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="13ed9-219">Webhook URL</span></span> |<span data-ttu-id="13ed9-220">웹후크의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-220">The URL of the webhook.</span></span> |
| <span data-ttu-id="13ed9-221">사용자 지정 JSON 페이로드 포함</span><span class="sxs-lookup"><span data-stu-id="13ed9-221">Include custom JSON payload</span></span> |<span data-ttu-id="13ed9-222">기본 페이로드를 사용자 지정 페이로드로 바꾸려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-222">Select this option if you want to replace the default payload with a custom payload.</span></span> |
| <span data-ttu-id="13ed9-223">사용자 지정 JSON 페이로드 입력</span><span class="sxs-lookup"><span data-stu-id="13ed9-223">Enter your custom JSON payload</span></span> |<span data-ttu-id="13ed9-224">웹후크에 대한 사용자 지정 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-224">The custom payload for the webhook.</span></span>  <span data-ttu-id="13ed9-225">자세한 내용은 이전 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13ed9-225">See previous section for details.</span></span> |

#### <a name="runbook-actions"></a><span data-ttu-id="13ed9-226">Runbook 작업</span><span class="sxs-lookup"><span data-stu-id="13ed9-226">Runbook actions</span></span>
<span data-ttu-id="13ed9-227">Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-227">Runbook actions start a runbook in Azure Automation.</span></span> 

>[!NOTE]
> <span data-ttu-id="13ed9-228">이 작업을 활성화하려면 작업 영역에 자동화 솔루션이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-228">You must have the Automation solution installed in your workspace for this action to be enabled.</span></span> 


| <span data-ttu-id="13ed9-229">속성</span><span class="sxs-lookup"><span data-stu-id="13ed9-229">Property</span></span> | <span data-ttu-id="13ed9-230">설명</span><span class="sxs-lookup"><span data-stu-id="13ed9-230">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="13ed9-231">Runbook</span><span class="sxs-lookup"><span data-stu-id="13ed9-231">Runbook</span></span> | <span data-ttu-id="13ed9-232">경고가 트리거될 때 Azure 자동화 Runbook을 시작하려면 **예** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-232">Specify **Yes** if you want to start an Azure Automation runbook when the alert is triggered.</span></span>  |
| <span data-ttu-id="13ed9-233">Automation 계정</span><span class="sxs-lookup"><span data-stu-id="13ed9-233">Automation account</span></span> | <span data-ttu-id="13ed9-234">Runbook을 선택할 자동화 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-234">Specifies the Automation account that runbooks are selected from.</span></span>  <span data-ttu-id="13ed9-235">작업 영역에 연결된 작업 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-235">This is the Action account that's linked to the workspace.</span></span> |
| <span data-ttu-id="13ed9-236">Runbook 선택</span><span class="sxs-lookup"><span data-stu-id="13ed9-236">Select a runbook</span></span> | <span data-ttu-id="13ed9-237">경고가 생성될 때 시작하려는 Runbook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-237">Select the runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="13ed9-238">실행</span><span class="sxs-lookup"><span data-stu-id="13ed9-238">Run on</span></span> | <span data-ttu-id="13ed9-239">클라우드에서 Runbook을 실행하려면 **Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-239">Select **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="13ed9-240">[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )가 설치된 에이전트에서 Runbook을 실행할 **Hybrid Worker**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-240">Select **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |




## <a name="next-steps"></a><span data-ttu-id="13ed9-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13ed9-241">Next steps</span></span>
* <span data-ttu-id="13ed9-242">SCOM(System Center Operations Manager)에서 수집한 경고와 함께 Log Analytics에서 만든 경고를 분석하려면 [경고 관리 솔루션](log-analytics-solution-alert-management.md) 을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-242">Install the [Alert Management solution](log-analytics-solution-alert-management.md) to analyze alerts created in Log Analytics along with alerts collected from System Center Operations Manager (SCOM).</span></span>
* <span data-ttu-id="13ed9-243">경고를 생성할 수 있는 [로그 검색](log-analytics-log-searches.md) 에 대해 자세한 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-243">Read more about [log searches](log-analytics-log-searches.md) that can generate alerts.</span></span>
* <span data-ttu-id="13ed9-244">경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-244">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
* <span data-ttu-id="13ed9-245">경고에 의해 식별된 문제를 수정하는 [Azure 자동화의 Runbook](https://azure.microsoft.com/documentation/services/automation) 을 작성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="13ed9-245">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>


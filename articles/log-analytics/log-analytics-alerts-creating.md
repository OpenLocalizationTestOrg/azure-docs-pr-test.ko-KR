---
title: "OMS 로그 분석에서 aaaCreating 경고 | Microsoft Docs"
description: "로그 분석에 OMS 리포지토리에 중요 한 정보를 식별 및 수 사전 문제점을 알려 경고나 작업 tooattempt toocorrect 호출을 합니다.  이 문서에서는 어떻게 toocreate 경고 규칙 및 세부 정보 hello 다양 한 작업 취할 수를 설명 합니다."
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
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a><span data-ttu-id="2d995-104">Log Analytics에서 경고 규칙 작업</span><span class="sxs-lookup"><span data-stu-id="2d995-104">Working with alert rules in Log Analytics</span></span>
<span data-ttu-id="2d995-105">경고는 일정한 간격으로 로그 검색을 자동으로 실행하는 경고 규칙에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-105">Alerts are created by alert rules that automatically run log searches at regular intervals.</span></span>  <span data-ttu-id="2d995-106">hello 결과 특정 조건과 일치 하는 경우 경고는 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-106">They create an alert record if hello results match particular criteria.</span></span>  <span data-ttu-id="2d995-107">hello 규칙 수 후 자동으로 하나를 실행 하거나 더 많은 작업 tooproactively hello 경고의 알림을 또는 다른 프로세스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-107">hello rule can then automatically run one or more actions tooproactively notify you of hello alert or invoke another process.</span></span>   

<span data-ttu-id="2d995-108">이 문서는 hello 프로세스 toocreate에 설명 하 고 hello OMS 포털을 사용 하 여 경고 규칙을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-108">This article describes hello processes toocreate and edit alert rules using hello OMS portal.</span></span>  <span data-ttu-id="2d995-109">Hello 다양 한 설정 및 tooimplement 논리 필요한 하는 방법에 대 한 세부 정보를 참조 하십시오. [로그 분석에서 경고 이해](log-analytics-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-109">For details about hello different settings and how tooimplement required logic, see [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

>[!NOTE]
> <span data-ttu-id="2d995-110">현재 만들 하거나 hello Azure 포털을 사용 하 여 경고 규칙을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-110">You cannot currently create or modify an alert rule using hello Azure portal.</span></span> 

## <a name="create-an-alert-rule"></a><span data-ttu-id="2d995-111">경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2d995-111">Create an alert rule</span></span>

<span data-ttu-id="2d995-112">로그를 만들어 시작 hello OMS 포털을 사용 하 여 경고 규칙을 toocreate hello 경고를 호출 해야 하는 hello 레코드를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-112">toocreate an alert rule using hello OMS portal, you start by creating a log search for hello records that should invoke hello alert.</span></span>  <span data-ttu-id="2d995-113">hello **경고** 만들고 hello 경고 규칙을 구성할 수 있도록 단추를 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-113">hello **Alert** button will then be available so you can create and configure hello alert rule.</span></span>

>[!NOTE]
> <span data-ttu-id="2d995-114">현재 OMS 작업 영역에서 최대 250개의 경고 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-114">A maximum of 250 alert rules can currently be created in an OMS workspace.</span></span> 

1. <span data-ttu-id="2d995-115">Hello OMS 개요 페이지에서 클릭 **로그 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-115">From hello OMS Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="2d995-116">새 로그 검색 쿼리를 만들거나 저장된 로그 검색을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-116">Either create a new log search query or select a saved log search.</span></span> 
3. <span data-ttu-id="2d995-117">클릭 **경고** hello 페이지 tooopen hello의 hello 위쪽 **경고 규칙 추가** 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-117">Click **Alert** at hello top of hello page tooopen hello **Add Alert Rule** screen.</span></span>
4. <span data-ttu-id="2d995-118">구성 정보를 사용 하는 hello 경고 규칙 [경고 규칙의 세부 정보](#details-of-alert-rules) 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-118">Configure hello alert rule using information in [Details of alert rules](#details-of-alert-rules) below.</span></span>
6. <span data-ttu-id="2d995-119">클릭 **저장** toocomplete hello 경고 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-119">Click **Save** toocomplete hello alert rule.</span></span>  <span data-ttu-id="2d995-120">실행을 즉시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-120">It will start running immediately.</span></span>


## <a name="edit-an-alert-rule"></a><span data-ttu-id="2d995-121">경고 규칙 편집</span><span class="sxs-lookup"><span data-stu-id="2d995-121">Edit an alert rule</span></span>
<span data-ttu-id="2d995-122">Hello에서 모든 경고 규칙의 목록을 가져올 수 있습니다 **경고** 로그 분석에서 메뉴 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-122">You can get a list of all alert rules in hello **Alerts** menu in Log Analytics **Settings**.</span></span>  

![경고 관리](./media/log-analytics-alerts/configure.png)

1. <span data-ttu-id="2d995-124">Hello OMS 콘솔 선택 hello에 **설정** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-124">In hello OMS console select hello **Settings** tile.</span></span>
2. <span data-ttu-id="2d995-125">**경고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-125">Select **Alerts**.</span></span>

<span data-ttu-id="2d995-126">이 뷰에서 여러 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-126">You can perform multiple actions from this view.</span></span>

* <span data-ttu-id="2d995-127">규칙을 사용 하지 않도록 선택 하 여 **오프** 다음 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-127">Disable a rule by selecting **Off** next tooit.</span></span>
* <span data-ttu-id="2d995-128">Hello 연필 아이콘 다음 tooit를 클릭 하 여 경고 규칙을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-128">Edit an alert rule by clicking hello pencil icon next tooit.</span></span>
* <span data-ttu-id="2d995-129">Hello를 클릭 하 여 경고 규칙을 제거할 **X** 다음 tooit 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-129">Remove an alert rule by clicking hello **X** icon next tooit.</span></span> 

## <a name="details-of-alert-rules"></a><span data-ttu-id="2d995-130">경고 규칙의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2d995-130">Details of alert rules</span></span>
<span data-ttu-id="2d995-131">Hello를 사용 하 여 작업할 만들거나 hello OMS 포털의 경고 규칙을 편집할 때 **경고 규칙 추가** 또는 **경고 규칙 편집** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2d995-131">When you create or edit an alert rule in hello OMS portal, you work with hello **Add Alert Rule** or **Edit Alert Rule** page.</span></span>  <span data-ttu-id="2d995-132">다음 표에서 hello hello 필드가이 화면에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-132">hello following tables describe hello fields in this screen.</span></span>

![경고 규칙](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a><span data-ttu-id="2d995-134">경고 정보</span><span class="sxs-lookup"><span data-stu-id="2d995-134">Alert information</span></span>
<span data-ttu-id="2d995-135">이 hello 경고 규칙 및 생성 하는 hello 경고에 대 한 기본 설정.</span><span class="sxs-lookup"><span data-stu-id="2d995-135">These are basic settings for hello alert rule and hello alerts it creates.</span></span>

| <span data-ttu-id="2d995-136">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-136">Property</span></span> | <span data-ttu-id="2d995-137">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-137">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-138">이름</span><span class="sxs-lookup"><span data-stu-id="2d995-138">Name</span></span> | <span data-ttu-id="2d995-139">고유 이름 tooidentify hello 경고 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-139">Unique name tooidentify hello alert rule.</span></span> <span data-ttu-id="2d995-140">이 이름은 hello 규칙에 의해 생성 된 모든 경고에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-140">This name is included in any alerts created by hello rule.</span></span>  |
| <span data-ttu-id="2d995-141">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-141">Description</span></span> | <span data-ttu-id="2d995-142">Hello 경고 규칙의 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-142">Optional description of hello alert rule.</span></span> |
| <span data-ttu-id="2d995-143">심각도</span><span class="sxs-lookup"><span data-stu-id="2d995-143">Severity</span></span> |<span data-ttu-id="2d995-144">이 규칙에 의해 생성된 모든 경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-144">Severity of any alerts created by this rule.</span></span> |

### <a name="search-query-and-time-window"></a><span data-ttu-id="2d995-145">검색 쿼리 및 기간</span><span class="sxs-lookup"><span data-stu-id="2d995-145">Search query and time window</span></span>
<span data-ttu-id="2d995-146">모든 경고를 생성 하면 평가 toodetermine 있는 hello 레코드를 반환 하는 hello 검색 쿼리 및 시간 창.</span><span class="sxs-lookup"><span data-stu-id="2d995-146">hello search query and time window that return hello records that are evaluated toodetermine if any alerts should be created.</span></span>

| <span data-ttu-id="2d995-147">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-147">Property</span></span> | <span data-ttu-id="2d995-148">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-148">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-149">검색 쿼리</span><span class="sxs-lookup"><span data-stu-id="2d995-149">Search query</span></span> | <span data-ttu-id="2d995-150">이것은 실행 되는 hello 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-150">This is hello query that will be run.</span></span>  <span data-ttu-id="2d995-151">이 쿼리에서 반환 된 hello 레코드 경고가 만들어지고 여부를 사용 하는 toodetermine 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-151">hello records returned by this query will be used toodetermine whether an alert is created.</span></span><br><br><span data-ttu-id="2d995-152">선택 **현재 검색 쿼리 사용** toouse 현재 쿼리 hello 하거나 기존에 저장 된 검색 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-152">Select **Use current search query** toouse hello current query or select an existing saved search from hello list.</span></span>  <span data-ttu-id="2d995-153">hello 쿼리 구문은 수정할 수 있는 필요한 경우 hello 텍스트 상자에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-153">hello query syntax is provided in hello text box where you can modify it if necessary.</span></span> |
| <span data-ttu-id="2d995-154">기간</span><span class="sxs-lookup"><span data-stu-id="2d995-154">Time window</span></span> |<span data-ttu-id="2d995-155">Hello 쿼리에 대 한 hello 시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-155">Specifies hello time range for hello query.</span></span>  <span data-ttu-id="2d995-156">hello 쿼리는 현재 시간 hello이이 범위 내에서 생성 된 레코드만 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-156">hello query returns only records that were created within this range of  hello current time.</span></span>  <span data-ttu-id="2d995-157">이는 5 분에서 24 시간 사이의 임의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-157">This can be any value between 5 minutes and 24 hours.</span></span>  <span data-ttu-id="2d995-158">알림 빈도 보다 크거나 같은 toohello 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-158">It should be greater than or equal toohello alert frequency.</span></span>  <br><br> <span data-ttu-id="2d995-159">예를 들어 hello too60 분과 hello 쿼리 창을 설정 된 시간에 실행 된 경우 오후 1 시 15 분 오후 12시 15분와 오후 1시 15분 사이 레코드만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-159">For example, If hello time window is set too60 minutes, and hello query is run at 1:15 PM, only records created between 12:15 PM and 1:15 PM will be returned.</span></span> |

<span data-ttu-id="2d995-160">Hello 경고 규칙에 대 한 hello 기간을 지정할 때는 hello 해당 기간에 대 한 hello 검색 조건과 일치 하는 기존 레코드 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-160">When you provide hello time window for hello alert rule, hello number of existing records that match hello search criteria for that time window will be displayed.</span></span>  <span data-ttu-id="2d995-161">제공 하는 hello 빈도 확인할 수 있습니다이 hello 예상 되는 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-161">This can help you determine hello frequency that will give you hello number of results that you expect.</span></span>

### <a name="schedule"></a><span data-ttu-id="2d995-162">일정</span><span class="sxs-lookup"><span data-stu-id="2d995-162">Schedule</span></span>
<span data-ttu-id="2d995-163">Hello 검색 쿼리는 실행 빈도 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-163">Defines how often hello search query is run.</span></span>

| <span data-ttu-id="2d995-164">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-164">Property</span></span> | <span data-ttu-id="2d995-165">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-165">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-166">경고 빈도</span><span class="sxs-lookup"><span data-stu-id="2d995-166">Alert frequency</span></span> | <span data-ttu-id="2d995-167">얼마나 자주 hello 쿼리 실행 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-167">Specifies how often hello query should be run.</span></span> <span data-ttu-id="2d995-168">5 분에서 24 시간 사이의 임의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-168">Can be any value between 5 minutes and 24 hours.</span></span> <span data-ttu-id="2d995-169">Hello 기간 보다 작은 tooor 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-169">Should be equal tooor less than hello time window.</span></span>  <span data-ttu-id="2d995-170">Hello 값 hello 기간 보다 큰 경우 레코드가 누락 될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-170">If hello value is greater than hello time window, then you risk records being missed.</span></span><br><br><span data-ttu-id="2d995-171">예를 들어 30분의 기간과 60분의 빈도를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-171">For example, consider a time window of 30 minutes and a frequency of 60 minutes.</span></span>  <span data-ttu-id="2d995-172">Hello 쿼리 1:00에 실행 된 경우 오후 12시 30분 1시 사이 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-172">If hello query is run at 1:00, it returns records between 12:30 and 1:00 PM.</span></span>  <span data-ttu-id="2d995-173">hello는 hello 쿼리는 실행 하는 다음에 2:00 때 1시 30분 2시 사이 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-173">hello next time hello query would run is 2:00 when it would return records between 1:30 and 2:00.</span></span>  <span data-ttu-id="2d995-174">1:00 및 1:30 사이에 생성된 레코드는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-174">Any records created between 1:00 and 1:30 would never be evaluated.</span></span> |


### <a name="generate-alert-based-on"></a><span data-ttu-id="2d995-175">경고 생성 조건</span><span class="sxs-lookup"><span data-stu-id="2d995-175">Generate alert based on</span></span>
<span data-ttu-id="2d995-176">Hello 평가 되는 경우 경고 hello 검색 쿼리 toodetermine의 hello 결과 대해 링크 조건을 생성할 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-176">Defines hello criteria that will be evaluated against hello results of hello search query toodetermine if an alert should be created.</span></span>  <span data-ttu-id="2d995-177">이러한 세부 사항을 선택 하는 경고 규칙의 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-177">These details will be different depending on hello type of alert rule that you select.</span></span>  <span data-ttu-id="2d995-178">다른 경고 규칙 유형을 hello에 대 한 세부 정보를 얻을 수 있습니다 [로그 분석에서 경고 이해](log-analytics-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-178">You can get details for hello different alert rule types from [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

| <span data-ttu-id="2d995-179">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-179">Property</span></span> | <span data-ttu-id="2d995-180">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-180">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-181">알림 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="2d995-181">Suppress alerts</span></span> | <span data-ttu-id="2d995-182">억제 (suppression) hello 경고 규칙에 대 한을 설정 하면 새 경고를 만든 후 정의 된 기간에 대 한 hello 규칙에 대 한 작업을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-182">When you turn on suppression for hello alert rule, actions for hello rule are disabled for a defined length of time after creating a new alert.</span></span> <span data-ttu-id="2d995-183">hello 규칙 실행 되 고 hello 조건을 충족할 경우 경고 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-183">hello rule is still running and will create alert records if hello criteria is met.</span></span> <span data-ttu-id="2d995-184">중복 작업을 실행 하지 않고 toocorrect hello 문제 시간 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-184">This is tooallow you time toocorrect hello problem without running duplicate actions.</span></span> |

#### <a name="number-of-results-alert-rules"></a><span data-ttu-id="2d995-185">결과 수 경고 규칙</span><span class="sxs-lookup"><span data-stu-id="2d995-185">Number of results alert rules</span></span>

| <span data-ttu-id="2d995-186">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-186">Property</span></span> | <span data-ttu-id="2d995-187">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-187">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-188">결과의 수</span><span class="sxs-lookup"><span data-stu-id="2d995-188">Number of results</span></span> |<span data-ttu-id="2d995-189">Hello hello 쿼리에서 반환 된 레코드 수가 경고가 만들어지고 **보다 큰** 또는 **미만** hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-189">An alert is created if hello number of records returned by hello query is either **greater than** or **less than** hello value you provide.</span></span>  |

#### <a name="metric-measurement-alert-rules"></a><span data-ttu-id="2d995-190">미터법 경고 규칙</span><span class="sxs-lookup"><span data-stu-id="2d995-190">Metric measurement alert rules</span></span>

| <span data-ttu-id="2d995-191">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-191">Property</span></span> | <span data-ttu-id="2d995-192">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-192">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-193">집계 값</span><span class="sxs-lookup"><span data-stu-id="2d995-193">Aggregate value</span></span> | <span data-ttu-id="2d995-194">Hello 결과의 각 집계 값 toobe를 초과 해야 하는 임계값 위반으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-194">Threshold value that each aggregate value in hello results must exceed toobe considered a breach.</span></span> |
| <span data-ttu-id="2d995-195">경고 트리거 조건</span><span class="sxs-lookup"><span data-stu-id="2d995-195">Trigger alert based on</span></span> | <span data-ttu-id="2d995-196">hello 생성 하는 경고 toobe에 대 한 위반 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-196">hello number of breaches for an alert toobe created.</span></span>  <span data-ttu-id="2d995-197">지정할 수 있습니다 **위반 총** hello 결과에서 즘 조합에 대 한 설정 또는 **연속 위반** 위반 hello toorequire 연속 샘플에서 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-197">You can specify **Total breaches** for any combination of breaches across hello results set or **Consecutive breaches** toorequire that hello breaches must occur in consecutive samples.</span></span> |

### <a name="actions"></a><span data-ttu-id="2d995-198">작업</span><span class="sxs-lookup"><span data-stu-id="2d995-198">Actions</span></span>
<span data-ttu-id="2d995-199">경고 규칙을 항상 만듭니다는 [레코드 경고](#alert-records) hello 임계값을 충족 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2d995-199">Alert rules will always create an [alert record](#alert-records) when hello threshold is met.</span></span>  <span data-ttu-id="2d995-200">또한 정의할 수 있습니다 또는 전자 메일을 보낼 runbook 시작 등 자세한 응답 toobe 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-200">You can also define one or more responses toobe run such as sending an email or starting a runbook.</span></span>



#### <a name="email-actions"></a><span data-ttu-id="2d995-201">전자 메일 작업</span><span class="sxs-lookup"><span data-stu-id="2d995-201">Email actions</span></span>
<span data-ttu-id="2d995-202">전자 메일 작업 hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-202">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>

| <span data-ttu-id="2d995-203">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-203">Property</span></span> | <span data-ttu-id="2d995-204">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-204">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-205">메일 알림</span><span class="sxs-lookup"><span data-stu-id="2d995-205">Email notification</span></span> |<span data-ttu-id="2d995-206">지정 **예** hello 경고가 트리거될 때 전송 되는 전자 메일 toobe 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="2d995-206">Specify **Yes** if you want an email toobe sent when hello alert is triggered.</span></span> |
| <span data-ttu-id="2d995-207">제목</span><span class="sxs-lookup"><span data-stu-id="2d995-207">Subject</span></span> |<span data-ttu-id="2d995-208">Hello 전자 메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-208">Subject in hello email.</span></span>  <span data-ttu-id="2d995-209">Hello 메일의 본문 hello를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-209">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="2d995-210">받는 사람</span><span class="sxs-lookup"><span data-stu-id="2d995-210">Recipients</span></span> |<span data-ttu-id="2d995-211">모든 전자 메일 받는 사람의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-211">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="2d995-212">세미콜론 (;)를 사용 하 여 여러 개의 주소가 다음 별도 hello 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-212">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="2d995-213">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="2d995-213">Webhook actions</span></span>
<span data-ttu-id="2d995-214">Webhook 작업 tooinvoke 단일 HTTP POST 요청을 통해 외부 프로세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-214">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>

| <span data-ttu-id="2d995-215">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-215">Property</span></span> | <span data-ttu-id="2d995-216">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-216">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-217">웹후크</span><span class="sxs-lookup"><span data-stu-id="2d995-217">Webhook</span></span> |<span data-ttu-id="2d995-218">지정 **예** hello 경고가 트리거될 때 toocall 여 webhook을 사용할지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-218">Specify **Yes** if you want toocall a webhook when hello alert is triggered.</span></span> |
| <span data-ttu-id="2d995-219">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="2d995-219">Webhook URL</span></span> |<span data-ttu-id="2d995-220">hello webhook의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-220">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="2d995-221">사용자 지정 JSON 페이로드 포함</span><span class="sxs-lookup"><span data-stu-id="2d995-221">Include custom JSON payload</span></span> |<span data-ttu-id="2d995-222">사용자 지정 페이로드를 사용한 tooreplace hello 기본 페이로드를 원하는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-222">Select this option if you want tooreplace hello default payload with a custom payload.</span></span> |
| <span data-ttu-id="2d995-223">사용자 지정 JSON 페이로드 입력</span><span class="sxs-lookup"><span data-stu-id="2d995-223">Enter your custom JSON payload</span></span> |<span data-ttu-id="2d995-224">hello hello webhook에 대 한 사용자 지정 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-224">hello custom payload for hello webhook.</span></span>  <span data-ttu-id="2d995-225">자세한 내용은 이전 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d995-225">See previous section for details.</span></span> |

#### <a name="runbook-actions"></a><span data-ttu-id="2d995-226">Runbook 작업</span><span class="sxs-lookup"><span data-stu-id="2d995-226">Runbook actions</span></span>
<span data-ttu-id="2d995-227">Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-227">Runbook actions start a runbook in Azure Automation.</span></span> 

>[!NOTE]
> <span data-ttu-id="2d995-228">Hello 자동화 솔루션이이 동작 toobe 사용에 대 한 작업 영역에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-228">You must have hello Automation solution installed in your workspace for this action toobe enabled.</span></span> 


| <span data-ttu-id="2d995-229">속성</span><span class="sxs-lookup"><span data-stu-id="2d995-229">Property</span></span> | <span data-ttu-id="2d995-230">설명</span><span class="sxs-lookup"><span data-stu-id="2d995-230">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="2d995-231">Runbook</span><span class="sxs-lookup"><span data-stu-id="2d995-231">Runbook</span></span> | <span data-ttu-id="2d995-232">지정 **예** hello 경고가 트리거될 때 toostart Azure 자동화 runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-232">Specify **Yes** if you want toostart an Azure Automation runbook when hello alert is triggered.</span></span>  |
| <span data-ttu-id="2d995-233">Automation 계정</span><span class="sxs-lookup"><span data-stu-id="2d995-233">Automation account</span></span> | <span data-ttu-id="2d995-234">Hello runbook에서 선택 된 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-234">Specifies hello Automation account that runbooks are selected from.</span></span>  <span data-ttu-id="2d995-235">연결 된 작업 영역 toohello hello 작업 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-235">This is hello Action account that's linked toohello workspace.</span></span> |
| <span data-ttu-id="2d995-236">Runbook 선택</span><span class="sxs-lookup"><span data-stu-id="2d995-236">Select a runbook</span></span> | <span data-ttu-id="2d995-237">경고를 만들 때 않겠다고 toostart hello runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-237">Select hello runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="2d995-238">실행</span><span class="sxs-lookup"><span data-stu-id="2d995-238">Run on</span></span> | <span data-ttu-id="2d995-239">선택 **Azure** hello 클라우드에서 toorun hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-239">Select **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="2d995-240">선택 **Hybrid worker** 와 에이전트에서 toorun hello runbook [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-240">Select **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |




## <a name="next-steps"></a><span data-ttu-id="2d995-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d995-241">Next steps</span></span>
* <span data-ttu-id="2d995-242">Hello 설치 [경고 관리 솔루션](log-analytics-solution-alert-management.md) tooanalyze 경고 경고와 함께 로그 분석에서 만든 System Center Operations Manager (SCOM)에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-242">Install hello [Alert Management solution](log-analytics-solution-alert-management.md) tooanalyze alerts created in Log Analytics along with alerts collected from System Center Operations Manager (SCOM).</span></span>
* <span data-ttu-id="2d995-243">경고를 생성할 수 있는 [로그 검색](log-analytics-log-searches.md) 에 대해 자세한 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-243">Read more about [log searches](log-analytics-log-searches.md) that can generate alerts.</span></span>
* <span data-ttu-id="2d995-244">경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-244">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
* <span data-ttu-id="2d995-245">자세한 내용은 어떻게 toowrite [Azure 자동화의 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 문제를 경고로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d995-245">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>


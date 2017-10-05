---
title: "OMS Log Analytics 경고 REST API 사용"
description: "Log Analytics 경고 REST API를 사용하여 OMS(Operations Management Suite)의 일부인 Log Analytics에서 경고를 만들고 관리할 수 있습니다.  이 문서에서는 다음 작업을 수행하기 위한 API 및 여러 예제의 세부 정보를 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="b6d82-104">REST API로 Log Analytics에서 경고 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="b6d82-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="b6d82-105">Log Analytics 경고 REST API를 사용하여 OMS(Operations Management Suite)에서 경고를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="b6d82-106">이 문서에서는 다음 작업을 수행하기 위한 API 및 여러 예제의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="b6d82-107">Log Analytics 검색 REST API는 RESTful이며 Azure Resource Manager REST API를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="b6d82-108">이 문서에서 API가 Azure Resource Manager API를 호출하여 단순화하는 공개 소스 명령줄 도구인 [ARMClient](https://github.com/projectkudu/ARMClient)를 사용하여 PowerShell 명령줄에서 액세스하는 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="b6d82-109">ARMClient 및 PowerShell의 사용은 Log Analytics 검색 API에 액세스하는 다양한 옵션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="b6d82-110">이러한 도구를 사용하면 RESTful Azure Resource Manager API를 통해 OMS 작업 영역을 호출하고 작업 영역 내에서 검색 명령을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="b6d82-111">API은 JSON 형식으로 검색 결과를 출력하여 다양한 프로그래밍 방식으로 검색 결과를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6d82-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b6d82-112">Prerequisites</span></span>
<span data-ttu-id="b6d82-113">현재 Log Analytics에 저장된 검색을 사용해서만 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="b6d82-114">자세한 내용은 [로그 검색 REST API](log-analytics-log-search-api.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6d82-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="b6d82-115">일정</span><span class="sxs-lookup"><span data-stu-id="b6d82-115">Schedules</span></span>
<span data-ttu-id="b6d82-116">저장된 검색은 하나 이상의 일정을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="b6d82-117">일정은 검색이 실행되는 빈도 및 조건이 식별되는 기간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="b6d82-118">일정은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="b6d82-119">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-119">Property</span></span> | <span data-ttu-id="b6d82-120">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-121">간격</span><span class="sxs-lookup"><span data-stu-id="b6d82-121">Interval</span></span> |<span data-ttu-id="b6d82-122">검색이 실행되는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-122">How often the search is run.</span></span> <span data-ttu-id="b6d82-123">분 단위로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-123">Measured in minutes.</span></span> |
| <span data-ttu-id="b6d82-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="b6d82-124">QueryTimeSpan</span></span> |<span data-ttu-id="b6d82-125">조건이 평가되는 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="b6d82-126">간격보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="b6d82-127">분 단위로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-127">Measured in minutes.</span></span> |
| <span data-ttu-id="b6d82-128">버전</span><span class="sxs-lookup"><span data-stu-id="b6d82-128">Version</span></span> |<span data-ttu-id="b6d82-129">사용 중인 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-129">The API version being used.</span></span>  <span data-ttu-id="b6d82-130">현재 항상 1로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="b6d82-131">예를 들어 간격이 15 분이고 Timespan이 30 분인 이벤트 쿼리를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="b6d82-132">이 경우 쿼리는 매 15 분마다 실행되며 조건이 30 분의 기간 동안 계속 True로 확인되었으면 경고가 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="b6d82-133">일정 검색</span><span class="sxs-lookup"><span data-stu-id="b6d82-133">Retrieving schedules</span></span>
<span data-ttu-id="b6d82-134">Get 메서드를 사용하여 저장된 검색에 대한 모든 일정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="b6d82-135">일정 ID와 Get 메서드를 사용하여 저장된 검색에 대한 특정 일정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="b6d82-136">다음은 일정에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="b6d82-137">일정 만들기</span><span class="sxs-lookup"><span data-stu-id="b6d82-137">Creating a schedule</span></span>
<span data-ttu-id="b6d82-138">고유 일정 ID와 Put 메서드를 사용하여 새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="b6d82-139">두 일정은 서로 다른 저장된 검색과 연결되었다 하더라도 동일한 ID를 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="b6d82-140">OMS 콘솔에서 일정을 만드는 경우 일정 ID에 대해 GUID가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d82-141">Log Analytics API를 사용하여 만든 저장된 모든 검색, 일정 및 작업의 이름은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="b6d82-142">일정 편집</span><span class="sxs-lookup"><span data-stu-id="b6d82-142">Editing a schedule</span></span>
<span data-ttu-id="b6d82-143">동일한 저장된 검색에 대해 기존 일정 ID와 Put 메서드를 사용하여 해당 일정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="b6d82-144">요청 본문에는 일정의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="b6d82-145">일정 삭제</span><span class="sxs-lookup"><span data-stu-id="b6d82-145">Deleting schedules</span></span>
<span data-ttu-id="b6d82-146">일정 ID와 함께 Delete 메서드를 사용하여 일정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="b6d82-147">actions</span><span class="sxs-lookup"><span data-stu-id="b6d82-147">Actions</span></span>
<span data-ttu-id="b6d82-148">일정이 여러 작업을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="b6d82-149">작업은 메일 보내기 또는 Runbook 시작과 같은 하나 이상의 수행할 프로세스를 정의하거나 검색 결과가 일부 조건과 일치하는 경우를 결정하는 임계값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="b6d82-150">일부 작업은 임계값을 만족할 때 프로세스가 수행되도록 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="b6d82-151">모든 작업은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="b6d82-152">서로 다른 유형의 경고는 아래에 설명하는 서로 다른 추가 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="b6d82-153">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-153">Property</span></span> | <span data-ttu-id="b6d82-154">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-155">형식</span><span class="sxs-lookup"><span data-stu-id="b6d82-155">Type</span></span> |<span data-ttu-id="b6d82-156">작업의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-156">Type of the action.</span></span>  <span data-ttu-id="b6d82-157">현재 가능한 값은 경고 및 웹후크입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="b6d82-158">이름</span><span class="sxs-lookup"><span data-stu-id="b6d82-158">Name</span></span> |<span data-ttu-id="b6d82-159">경고에 대한 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-159">Display name for the alert.</span></span> |
| <span data-ttu-id="b6d82-160">버전</span><span class="sxs-lookup"><span data-stu-id="b6d82-160">Version</span></span> |<span data-ttu-id="b6d82-161">사용 중인 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-161">The API version being used.</span></span>  <span data-ttu-id="b6d82-162">현재 항상 1로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="b6d82-163">작업 검색</span><span class="sxs-lookup"><span data-stu-id="b6d82-163">Retrieving actions</span></span>
<span data-ttu-id="b6d82-164">Get 메서드를 사용하여 일정에 대한 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="b6d82-165">작업 ID와 함께 Get 메서드를 사용하여 일정에 대한 특정 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="b6d82-166">작업 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="b6d82-166">Creating or editing actions</span></span>
<span data-ttu-id="b6d82-167">일정에 고유한 작업 ID와 Put 메서드를 사용하여 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="b6d82-168">OMS 콘솔에서 작업을 만드는 경우 GUID는 작업 ID에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d82-169">Log Analytics API를 사용하여 만든 저장된 모든 검색, 일정 및 작업의 이름은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="b6d82-170">동일한 저장된 검색에 대해 기존 작업 ID와 Put 메서드를 사용하여 해당 일정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="b6d82-171">요청 본문에는 일정의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="b6d82-172">새 작업을 만들기 위한 요청 형식은 작업 유형에 따라 다르므로 이러한 예제를 아래 섹션에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="b6d82-173">작업 삭제</span><span class="sxs-lookup"><span data-stu-id="b6d82-173">Deleting actions</span></span>
<span data-ttu-id="b6d82-174">작업 ID와 함께 Delete 메서드를 사용하여 작업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="b6d82-175">경고 작업</span><span class="sxs-lookup"><span data-stu-id="b6d82-175">Alert Actions</span></span>
<span data-ttu-id="b6d82-176">일정은 경고 작업을 한 개만 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="b6d82-177">경고 작업은 다음 표의 섹션 중 하나 이상을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="b6d82-178">아래에서 각 섹션을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="b6d82-179">섹션</span><span class="sxs-lookup"><span data-stu-id="b6d82-179">Section</span></span> | <span data-ttu-id="b6d82-180">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-181">임계값</span><span class="sxs-lookup"><span data-stu-id="b6d82-181">Threshold</span></span> |<span data-ttu-id="b6d82-182">작업이 실행되기 위한 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="b6d82-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="b6d82-183">EmailNotification</span></span> |<span data-ttu-id="b6d82-184">복수의 받는 사람에게 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="b6d82-185">재구성</span><span class="sxs-lookup"><span data-stu-id="b6d82-185">Remediation</span></span> |<span data-ttu-id="b6d82-186">Azure 자동화에서 식별된 문제의 해결을 시도하는 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="b6d82-187">임계값</span><span class="sxs-lookup"><span data-stu-id="b6d82-187">Thresholds</span></span>
<span data-ttu-id="b6d82-188">경고 작업은 임계값을 한 개만 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="b6d82-189">저장된 검색의 결과가 해당 검색과 연결된 작업의 임계값과 일치하는 경우 해당 작업의 다른 프로세스가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="b6d82-190">작업은 임계값을 포함하지 않은 다른 유형의 작업과 함께 사용할 수 있도록 하는 임계값만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="b6d82-191">임계값은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="b6d82-192">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-192">Property</span></span> | <span data-ttu-id="b6d82-193">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-194">연산자</span><span class="sxs-lookup"><span data-stu-id="b6d82-194">Operator</span></span> |<span data-ttu-id="b6d82-195">임계값 비교를 위한 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="b6d82-196">gt = 보다 큰</span><span class="sxs-lookup"><span data-stu-id="b6d82-196">gt = Greater Than</span></span> <br> <span data-ttu-id="b6d82-197">lt = 보다 작은</span><span class="sxs-lookup"><span data-stu-id="b6d82-197">lt = Less Than</span></span> |
| <span data-ttu-id="b6d82-198">값</span><span class="sxs-lookup"><span data-stu-id="b6d82-198">Value</span></span> |<span data-ttu-id="b6d82-199">임계값에 대한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-199">Value for the threshold.</span></span> |

<span data-ttu-id="b6d82-200">예를 들어 간격이 15 분이고 Timespan이 30 분이고 임계값이 10보다 큰 이벤트 쿼리를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="b6d82-201">이 경우 쿼리는 매 15 분마다 실행되며 경고는 30 분의 기간 동안 생성된 이벤트 10개를 반환하면 경고가 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="b6d82-202">다음은 임계값만 가진 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="b6d82-203">고유 작업 ID와 Put 메서드를 사용하여 일정에 대한 새 임계값 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="b6d82-204">고유 작업 ID와 Put 메서드를 사용하여 일정에 대한 임계값 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="b6d82-205">요청 본문에는 작업의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="b6d82-206">메일 알림</span><span class="sxs-lookup"><span data-stu-id="b6d82-206">Email Notification</span></span>
<span data-ttu-id="b6d82-207">전자 메일 알림은 한 명 이상의 받는 사람에게 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="b6d82-208">이들은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="b6d82-209">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-209">Property</span></span> | <span data-ttu-id="b6d82-210">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-211">받는 사람</span><span class="sxs-lookup"><span data-stu-id="b6d82-211">Recipients</span></span> |<span data-ttu-id="b6d82-212">메일 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-212">List of mail addresses.</span></span> |
| <span data-ttu-id="b6d82-213">제목</span><span class="sxs-lookup"><span data-stu-id="b6d82-213">Subject</span></span> |<span data-ttu-id="b6d82-214">메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-214">The subject of the mail.</span></span> |
| <span data-ttu-id="b6d82-215">첨부 파일</span><span class="sxs-lookup"><span data-stu-id="b6d82-215">Attachment</span></span> |<span data-ttu-id="b6d82-216">첨부 파일은 현재 지원되지 않으므로이에 대한 값은 항상 "없음"입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="b6d82-217">다음은 임계값을 가진 전자 메일 알림 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="b6d82-218">고유한 작업 ID와 함께 Put 메서드를 사용하여 일정에 대한 새 전자 메일 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="b6d82-219">다음 예제에서는 저장된 검색의 결과가 임계값을 초과하는 경우 전자 메일을 보내도록 임계값을 가진 전자 메일 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="b6d82-220">고유 작업 ID와 Put 메서드를 사용하여 일정에 대한 이메일 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="b6d82-221">요청 본문에는 작업의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="b6d82-222">수정 작업</span><span class="sxs-lookup"><span data-stu-id="b6d82-222">Remediation actions</span></span>
<span data-ttu-id="b6d82-223">수정은 경고에 의해 식별된 문제의 해결을 시도하는 Azure 자동화의 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="b6d82-224">수정 작업에 사용되는 Runbook에 대한 웹후크를 만든 다음 WebhookUri 속성에서 URI를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="b6d82-225">OMS 콘솔을 사용하여 이 작업을 만드는 경우 Runbook에 대해 새 웹후크가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="b6d82-226">수정은 다음 표의 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="b6d82-227">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-227">Property</span></span> | <span data-ttu-id="b6d82-228">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="b6d82-229">RunbookName</span></span> |<span data-ttu-id="b6d82-230">Runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-230">Name of the runbook.</span></span> <span data-ttu-id="b6d82-231">이는 OMS 작업 영역의 자동화 솔루션에서 구성한 자동화 계정의 게시된 Runbook과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="b6d82-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="b6d82-232">WebhookUri</span></span> |<span data-ttu-id="b6d82-233">웹후크의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-233">URI of the webhook.</span></span> |
| <span data-ttu-id="b6d82-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="b6d82-234">Expiry</span></span> |<span data-ttu-id="b6d82-235">웹후크의 만료 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="b6d82-236">웹후크에 대해 만료를 지정하지 않은 경우 이는 유효한 미래 날짜일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="b6d82-237">다음은 임계값을 가진 수정 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="b6d82-238">고유한 작업 ID와 함께 Put 메서드를 사용하여 일정에 대한 새 수정 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="b6d82-239">다음 예제에서는 저장된 검색의 결과가 임계값을 초과하는 경우 Runbook이 시작되도록 임계값을 가진 수정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="b6d82-240">고유 작업 ID와 Put 메서드를 사용하여 일정에 대한 수정 작업을 정정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="b6d82-241">요청 본문에는 작업의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="b6d82-242">예</span><span class="sxs-lookup"><span data-stu-id="b6d82-242">Example</span></span>
<span data-ttu-id="b6d82-243">다음은 새 전자 메일 알림을 만드는 전체 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="b6d82-244">이는 임계값 및 전자 메일을 포함하는 작업과 함께 새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="b6d82-245">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="b6d82-245">Webhook actions</span></span>
<span data-ttu-id="b6d82-246">웹후크 작업은 URL을 호출하고 선택적으로 보낼 페이로드를 제공하는 것으로 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="b6d82-247">이들은 웹후크에 대해 Azure 자동화 Runbook 이외의 프로세스를 호출할 수 있다는 것을 제외하고 수정 작업과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="b6d82-248">또한 원격 프로세스에 전달할 페이로드를 제공하는 추가 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="b6d82-249">웹후크 작업은 임계값을 갖지 않지만 대신에 임계값과 함께 경고 작업을 가진 일정에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="b6d82-250">임계값을 만족할 때 모두 실행될 복수의 웹후크 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="b6d82-251">웹후크 작업은 다음 표의 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="b6d82-252">속성</span><span class="sxs-lookup"><span data-stu-id="b6d82-252">Property</span></span> | <span data-ttu-id="b6d82-253">설명</span><span class="sxs-lookup"><span data-stu-id="b6d82-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6d82-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="b6d82-254">WebhookUri</span></span> |<span data-ttu-id="b6d82-255">메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-255">The subject of the mail.</span></span> |
| <span data-ttu-id="b6d82-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="b6d82-256">CustomPayload</span></span> |<span data-ttu-id="b6d82-257">웹후크에 보낼 사용자 지정 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="b6d82-258">형식은 예상하는 웹후크에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="b6d82-259">다음은 웹후크 작업 및 임계값을 가진 연결된 경고에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="b6d82-260">웹후크 작업 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="b6d82-260">Create or edit a webhook action</span></span>
<span data-ttu-id="b6d82-261">고유한 작업 ID와 함께 Put 메서드를 사용하여 일정에 대한 새 웹후크 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="b6d82-262">다음 예제에서는 저장된 검색의 결과가 임계값을 초과하는 경우 웹후크가 트리거되도록 웹후크 작업 및 임계값을 가진 웹후크 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="b6d82-263">고유 작업 ID와 Put 메서드를 사용하여 일정에 대한 웹후크 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="b6d82-264">요청 본문에는 작업의 etag가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="b6d82-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6d82-265">Next steps</span></span>
* <span data-ttu-id="b6d82-266">Log Analytics에서 [REST API를 사용하여 로그 검색을 수행](log-analytics-log-search-api.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6d82-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>


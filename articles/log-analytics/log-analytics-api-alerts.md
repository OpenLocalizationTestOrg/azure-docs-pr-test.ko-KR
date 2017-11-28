---
title: "aaaUsing OMS 로그 분석 경고 REST API"
description: "로그 분석 경고 REST API hello toocreate 있으며 Operations Management Suite (OMS)에 포함 된 로그 분석에서 경고를 관리 합니다.  이 문서는 다양 한 작업을 수행 하기 위한 hello API 및 몇 가지 예제에 대 한 세부 정보를 제공 합니다."
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
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="2a3f3-104">REST API로 Log Analytics에서 경고 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="2a3f3-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="2a3f3-105">로그 분석 경고 REST API hello toocreate 있으며 Operations Management Suite (OMS)에서 경고를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="2a3f3-106">이 문서는 다양 한 작업을 수행 하기 위한 hello API 및 몇 가지 예제에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="2a3f3-107">hello 로그 분석 검색 REST API는 RESTful 이며 Azure 리소스 관리자 REST API hello를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="2a3f3-108">이 문서의 예제를 확인할 수 hello API 사용 하 여 PowerShell 명령줄에서 액세스 되는 위치 [ARMClient](https://github.com/projectkudu/ARMClient), 호출을 간소화 하는 오픈 소스 명령줄 도구인 hello Azure 리소스 관리자 API입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="2a3f3-109">ARMClient 및 PowerShell 사용 hello 많은 옵션 tooaccess hello 로그 분석 검색 API 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="2a3f3-110">이러한 도구와 hello RESTful Azure 리소스 관리자 API toomake 호출 tooOMS 작업 영역을 사용 하 고 그 안에서 검색 명령을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="2a3f3-111">hello API은 JSON 형식으로 있도록 toouse hello 검색 결과 다양 한 방법으로 프로그래밍 방식으로 검색 결과 tooyou를 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a3f3-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a3f3-112">Prerequisites</span></span>
<span data-ttu-id="2a3f3-113">현재 Log Analytics에 저장된 검색을 사용해서만 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="2a3f3-114">Toohello 참조할 수 있습니다 [로그 검색 REST API](log-analytics-log-search-api.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="2a3f3-115">일정</span><span class="sxs-lookup"><span data-stu-id="2a3f3-115">Schedules</span></span>
<span data-ttu-id="2a3f3-116">저장된 검색은 하나 이상의 일정을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="2a3f3-117">hello 일정 정의 얼마나 자주 hello 검색은를 실행 하 고 hello 기준 hello 시간 마다 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="2a3f3-118">다음 표에 hello에 hello 속성을 포함 하는 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="2a3f3-119">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-119">Property</span></span> | <span data-ttu-id="2a3f3-120">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-121">간격</span><span class="sxs-lookup"><span data-stu-id="2a3f3-121">Interval</span></span> |<span data-ttu-id="2a3f3-122">얼마나 자주 hello 검색 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-122">How often hello search is run.</span></span> <span data-ttu-id="2a3f3-123">분 단위로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-123">Measured in minutes.</span></span> |
| <span data-ttu-id="2a3f3-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="2a3f3-124">QueryTimeSpan</span></span> |<span data-ttu-id="2a3f3-125">hello 시간 간격을 어떤 hello를 통해 조건 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="2a3f3-126">간격 보다 클 같은 tooor를 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="2a3f3-127">분 단위로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-127">Measured in minutes.</span></span> |
| <span data-ttu-id="2a3f3-128">버전</span><span class="sxs-lookup"><span data-stu-id="2a3f3-128">Version</span></span> |<span data-ttu-id="2a3f3-129">사용 되는 API 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-129">hello API version being used.</span></span>  <span data-ttu-id="2a3f3-130">현재이 항상 설정할 too1입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="2a3f3-131">예를 들어 간격이 15 분이고 Timespan이 30 분인 이벤트 쿼리를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="2a3f3-132">이 경우 hello 쿼리 15 분 마다 실행 하 고 hello 조건 30 분 기간 동안 tooresolve tootrue 계속 하는 경우 경고를 트리거할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="2a3f3-133">일정 검색</span><span class="sxs-lookup"><span data-stu-id="2a3f3-133">Retrieving schedules</span></span>
<span data-ttu-id="2a3f3-134">사용 하 여 hello 메서드 tooretrieve 저장된 된 검색에 대 한 모든 일정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="2a3f3-135">사용 하 여 hello 저장된 된 검색에 대 한 특정 일정을 일정 ID tooretrieve 사용 하 여 메서드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="2a3f3-136">다음은 일정에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="2a3f3-137">일정 만들기</span><span class="sxs-lookup"><span data-stu-id="2a3f3-137">Creating a schedule</span></span>
<span data-ttu-id="2a3f3-138">Hello Put 메서드를 사용 하 여 고유한 일정 ID toocreate 새 일정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="2a3f3-139">두 일정 없습니다는 hello 동일한 ID와 연결 된 다른 저장 된 검색 하는 경우에 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="2a3f3-140">Hello 일정 id는 GUID는 만들고 hello OMS 콘솔에서 일정을 만들 때</span><span class="sxs-lookup"><span data-stu-id="2a3f3-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3f3-141">저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="2a3f3-142">일정 편집</span><span class="sxs-lookup"><span data-stu-id="2a3f3-142">Editing a schedule</span></span>
<span data-ttu-id="2a3f3-143">동일한 저장 hello에 대 한 ID 검색 toomodify 예약 하는 기존 일정과 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="2a3f3-144">hello hello 요청 본문 hello 일정의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="2a3f3-145">일정 삭제</span><span class="sxs-lookup"><span data-stu-id="2a3f3-145">Deleting schedules</span></span>
<span data-ttu-id="2a3f3-146">일정 ID toodelete 일정 hello Delete 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="2a3f3-147">작업</span><span class="sxs-lookup"><span data-stu-id="2a3f3-147">Actions</span></span>
<span data-ttu-id="2a3f3-148">일정이 여러 작업을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="2a3f3-149">작업 하나 이상의 프로세스 tooperform 메일을 보내거나 runbook을 시작 하는 등을 정의할 수 있습니다 또는 hello 결과 검색 기준과 일치 하는 시기를 결정 하는 임계값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="2a3f3-150">Hello 임계값이 충족 되 면 hello 프로세스를 수행할 수 있도록 일부 작업을 모두 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="2a3f3-151">모든 작업에는 다음 표에 hello에 hello 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="2a3f3-152">서로 다른 유형의 경고는 아래에 설명하는 서로 다른 추가 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="2a3f3-153">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-153">Property</span></span> | <span data-ttu-id="2a3f3-154">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-155">형식</span><span class="sxs-lookup"><span data-stu-id="2a3f3-155">Type</span></span> |<span data-ttu-id="2a3f3-156">Hello 작업 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-156">Type of hello action.</span></span>  <span data-ttu-id="2a3f3-157">현재 hello 가능한 값은 경고 및 Webhook 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="2a3f3-158">이름</span><span class="sxs-lookup"><span data-stu-id="2a3f3-158">Name</span></span> |<span data-ttu-id="2a3f3-159">Hello 경고에 대 한 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="2a3f3-160">버전</span><span class="sxs-lookup"><span data-stu-id="2a3f3-160">Version</span></span> |<span data-ttu-id="2a3f3-161">사용 되는 API 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-161">hello API version being used.</span></span>  <span data-ttu-id="2a3f3-162">현재이 항상 설정할 too1입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="2a3f3-163">작업 검색</span><span class="sxs-lookup"><span data-stu-id="2a3f3-163">Retrieving actions</span></span>
<span data-ttu-id="2a3f3-164">사용 하 여 hello 메서드 tooretrieve 일정에 대 한 모든 작업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="2a3f3-165">사용 하 여 hello hello 동작 ID tooretrieve 메서드는 일정에 대 한 특정 동작을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="2a3f3-166">작업 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="2a3f3-166">Creating or editing actions</span></span>
<span data-ttu-id="2a3f3-167">작업 id는 고유 toohello 일정 toocreate 새 동작 ID와 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="2a3f3-168">Hello 동작 id는 GUID는 hello OMS 콘솔에서 작업을 만들 때</span><span class="sxs-lookup"><span data-stu-id="2a3f3-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3f3-169">저장 된 모든 검색, 일정 및 hello 로그 분석 API를 사용 하 여 만든 작업에 대 한 hello 이름은 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="2a3f3-170">동일한 저장 hello에 대 한 ID toomodify 예약 하는 검색 하는 기존 작업을 통해 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="2a3f3-171">hello hello 요청 본문 hello 일정의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="2a3f3-172">이 예에서는 hello 섹션 아래에 제공 되어 있으므로 새 동작을 만들기 위한 hello 요청 형식 동작 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="2a3f3-173">작업 삭제</span><span class="sxs-lookup"><span data-stu-id="2a3f3-173">Deleting actions</span></span>
<span data-ttu-id="2a3f3-174">Hello 동작 ID toodelete 동작 hello Delete 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="2a3f3-175">경고 작업</span><span class="sxs-lookup"><span data-stu-id="2a3f3-175">Alert Actions</span></span>
<span data-ttu-id="2a3f3-176">일정은 경고 작업을 한 개만 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="2a3f3-177">경고 작업에는 다음 표에 hello에 hello 섹션 중 하나 이상을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="2a3f3-178">아래에서 각 섹션을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="2a3f3-179">섹션</span><span class="sxs-lookup"><span data-stu-id="2a3f3-179">Section</span></span> | <span data-ttu-id="2a3f3-180">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-181">임계값</span><span class="sxs-lookup"><span data-stu-id="2a3f3-181">Threshold</span></span> |<span data-ttu-id="2a3f3-182">Hello 동작 실행 시기에 대 한 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="2a3f3-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="2a3f3-183">EmailNotification</span></span> |<span data-ttu-id="2a3f3-184">Toomultiple 받는 사람에 게 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="2a3f3-185">재구성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-185">Remediation</span></span> |<span data-ttu-id="2a3f3-186">Tooattempt toocorrect 식별 된 문제 Azure 자동화에서에서 runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="2a3f3-187">임계값</span><span class="sxs-lookup"><span data-stu-id="2a3f3-187">Thresholds</span></span>
<span data-ttu-id="2a3f3-188">경고 작업은 임계값을 한 개만 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="2a3f3-189">저장된 된 검색의 hello 결과가 해당 검색과 관련 된 동작에서 hello 임계값 일치 하는 경우 해당 작업의 다른 프로세스가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="2a3f3-190">작업은 임계값을 포함하지 않은 다른 유형의 작업과 함께 사용할 수 있도록 하는 임계값만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="2a3f3-191">임계값에는 다음 표에 hello에 hello 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="2a3f3-192">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-192">Property</span></span> | <span data-ttu-id="2a3f3-193">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-194">연산자</span><span class="sxs-lookup"><span data-stu-id="2a3f3-194">Operator</span></span> |<span data-ttu-id="2a3f3-195">Hello 임계값 비교 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="2a3f3-196">gt = 보다 큰</span><span class="sxs-lookup"><span data-stu-id="2a3f3-196">gt = Greater Than</span></span> <br> <span data-ttu-id="2a3f3-197">lt = 보다 작은</span><span class="sxs-lookup"><span data-stu-id="2a3f3-197">lt = Less Than</span></span> |
| <span data-ttu-id="2a3f3-198">값</span><span class="sxs-lookup"><span data-stu-id="2a3f3-198">Value</span></span> |<span data-ttu-id="2a3f3-199">Hello 임계값에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-199">Value for hello threshold.</span></span> |

<span data-ttu-id="2a3f3-200">예를 들어 간격이 15 분이고 Timespan이 30 분이고 임계값이 10보다 큰 이벤트 쿼리를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="2a3f3-201">이 경우 hello 쿼리 15 분 마다 실행 하 고 30 분 기간 동안 생성 된 이벤트 10 개 반환 되 면 경고를 트리거할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="2a3f3-202">다음은 임계값만 가진 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="2a3f3-203">일정에 대 한 고유한 작업 ID toocreate 새 임계값 동작으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="2a3f3-204">일정에 대 한 기존 동작 ID toomodify 임계값 동작으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="2a3f3-205">hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="2a3f3-206">메일 알림</span><span class="sxs-lookup"><span data-stu-id="2a3f3-206">Email Notification</span></span>
<span data-ttu-id="2a3f3-207">전자 메일 알림 메일 tooone 또는 더 많은 받는 사람에 게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="2a3f3-208">다음 표에 hello에 hello 속성 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="2a3f3-209">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-209">Property</span></span> | <span data-ttu-id="2a3f3-210">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-211">받는 사람</span><span class="sxs-lookup"><span data-stu-id="2a3f3-211">Recipients</span></span> |<span data-ttu-id="2a3f3-212">메일 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-212">List of mail addresses.</span></span> |
| <span data-ttu-id="2a3f3-213">제목</span><span class="sxs-lookup"><span data-stu-id="2a3f3-213">Subject</span></span> |<span data-ttu-id="2a3f3-214">hello 메일의 hello 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="2a3f3-215">첨부 파일</span><span class="sxs-lookup"><span data-stu-id="2a3f3-215">Attachment</span></span> |<span data-ttu-id="2a3f3-216">첨부 파일은 현재 지원되지 않으므로이에 대한 값은 항상 "없음"입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="2a3f3-217">다음은 임계값을 가진 전자 메일 알림 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="2a3f3-218">Hello Put 메서드는 일정에 대 한 고유한 작업 ID toocreate 새 전자 메일 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="2a3f3-219">hello 다음 예제에서는 만들므로 전자 메일 알림을 임계값과 hello 저장 된 검색의 hello 결과 hello 임계값을 초과 하는 경우 hello 메일이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="2a3f3-220">일정에 대 한 기존 동작 ID toomodify 전자 메일 동작으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="2a3f3-221">hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="2a3f3-222">수정 작업</span><span class="sxs-lookup"><span data-stu-id="2a3f3-222">Remediation actions</span></span>
<span data-ttu-id="2a3f3-223">재구성은 hello 경고도 식별 된 toocorrect hello 문제를 시도 하는 Azure 자동화에서 runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="2a3f3-224">수정 작업에 사용 된 hello runbook에 대 한 webhook을 만들고 hello WebhookUri 속성에서에서 hello URI를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="2a3f3-225">Hello OMS 콘솔을 사용 하 여이 작업을 만들 때 새 webhook hello runbook에 대 한 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="2a3f3-226">다음 표에 hello에 hello 속성을 포함 하는 재구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="2a3f3-227">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-227">Property</span></span> | <span data-ttu-id="2a3f3-228">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="2a3f3-229">RunbookName</span></span> |<span data-ttu-id="2a3f3-230">Hello runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-230">Name of hello runbook.</span></span> <span data-ttu-id="2a3f3-231">이 hello OMS 작업 영역에서 자동화 솔루션에에서 구성 된 hello 자동화 계정에서 게시 된 runbook을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="2a3f3-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="2a3f3-232">WebhookUri</span></span> |<span data-ttu-id="2a3f3-233">Hello webhook의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="2a3f3-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="2a3f3-234">Expiry</span></span> |<span data-ttu-id="2a3f3-235">hello 만료 날짜 및 시간 hello webhook입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="2a3f3-236">Hello webhook 없는 경우 만료 날짜, 유효한 모든 이후 날짜를 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="2a3f3-237">다음은 임계값을 가진 수정 작업에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="2a3f3-238">일정에 대 한 고유한 작업 ID toocreate 새 재구성 작업으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="2a3f3-239">hello 다음 예제에서는 만들므로 업데이트 관리 임계값과 hello 저장 된 검색의 hello 결과 hello 임계값을 초과 하는 경우 hello runbook이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="2a3f3-240">일정에 대 한 기존 동작 ID toomodify 재구성 작업으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="2a3f3-241">hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="2a3f3-242">예제</span><span class="sxs-lookup"><span data-stu-id="2a3f3-242">Example</span></span>
<span data-ttu-id="2a3f3-243">다음은 전체 예제 toocreate 새 전자 메일 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="2a3f3-244">이는 임계값 및 전자 메일을 포함하는 작업과 함께 새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="2a3f3-245">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="2a3f3-245">Webhook actions</span></span>
<span data-ttu-id="2a3f3-246">Webhook 작업 URL을 호출 하 여 선택적으로 전송 되는 페이로드 toobe 제공 하는 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="2a3f3-247">Azure 자동화 runbook 이외의 프로세스를 호출할 수 있는 webhook에 대 한 보관 점을 제외 하 고 서로 유사한 tooRemediation 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="2a3f3-248">또한 hello 페이로드 배달 toobe toohello 원격 프로세스를 제공 하는 중 추가 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="2a3f3-249">Webhook 작업 임계값 필요는 없지만 대신 추가할지 임계값과 경고 동작이 있는 tooa 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="2a3f3-250">모두 실행 되는 hello 임계값이 충족 하는 경우 여러 Webhook 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="2a3f3-251">다음 표에 hello에 hello 속성을 포함 하는 Webhook 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="2a3f3-252">속성</span><span class="sxs-lookup"><span data-stu-id="2a3f3-252">Property</span></span> | <span data-ttu-id="2a3f3-253">설명</span><span class="sxs-lookup"><span data-stu-id="2a3f3-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2a3f3-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="2a3f3-254">WebhookUri</span></span> |<span data-ttu-id="2a3f3-255">hello 메일의 hello 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="2a3f3-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="2a3f3-256">CustomPayload</span></span> |<span data-ttu-id="2a3f3-257">사용자 지정 페이로드 toobe toohello webhook을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="2a3f3-258">hello 형식 어떤 hello webhook 예상에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="2a3f3-259">다음은 웹후크 작업 및 임계값을 가진 연결된 경고에 대한 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="2a3f3-260">웹후크 작업 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="2a3f3-260">Create or edit a webhook action</span></span>
<span data-ttu-id="2a3f3-261">일정에 대 한 고유한 작업 ID toocreate 새 webhook 동작으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="2a3f3-262">hello 다음 예제에서는 Webhook 작업와 생성 경고 동작 임계값과 hello webhook hello 저장 된 검색의 hello 결과 hello 임계값을 초과할 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="2a3f3-263">일정에 대 한 기존 동작 ID toomodify webhook 작업으로 hello Put 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="2a3f3-264">hello hello 요청 본문 hello 동작의 hello etag를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="2a3f3-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a3f3-265">Next steps</span></span>
* <span data-ttu-id="2a3f3-266">사용 하 여 hello [REST API tooperform 로그 검색](log-analytics-log-search-api.md) 로그 분석에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3f3-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>


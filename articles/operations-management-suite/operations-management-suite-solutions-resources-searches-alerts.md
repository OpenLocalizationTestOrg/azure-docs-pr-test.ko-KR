---
title: "aaaSaved 검색 및 OMS 솔루션에서 경고 | Microsoft Docs"
description: "OMS의 솔루션 hello 솔루션에 의해 수집 된 로그 분석 tooanalyze 데이터에 저장 된 검색을 일반적으로 포함 됩니다.  경고 toonotify hello 사용자 정의 되었거나 자동으로 응답 tooa 중요 한 문제에서 작업을 수행 합니다.  이 문서에서는 어떻게 toodefine 로그 분석 검색 및 경고는 ARM 서식 파일에 저장 관리 솔루션에 포함 될 수 있도록 설명 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="cde52-105">로그 분석 추가 저장 된 검색 및 알림 tooOMS 관리 솔루션 (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="cde52-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="cde52-106">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="cde52-107">아래에 설명 된 모든 스키마 주체 toochange입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="cde52-108">[OMS의 관리 솔루션](operations-management-suite-solutions.md) 는 일반적으로 포함 [저장 된 검색](../log-analytics/log-analytics-log-searches.md) hello 솔루션에 의해 수집 된 로그 분석 tooanalyze 데이터에서입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="cde52-109">정의할 수도 있습니다 [경고](../log-analytics/log-analytics-alerts.md) toonotify 사용자 hello 또는 자동으로 응답 tooa 중요 한 문제에서 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="cde52-110">이 문서에서는 toodefine 로그 분석 검색 및 경고를 저장 하는 방법을 설명는 [리소스 관리 템플릿](../resource-manager-template-walkthrough.md) 에 포함 될 수 있으므로 [관리 솔루션](operations-management-suite-solutions-creating.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cde52-111">hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="cde52-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="cde52-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cde52-112">Prerequisites</span></span>
<span data-ttu-id="cde52-113">이 문서에서는 하 이미 방법을 잘 알고 너무 가정[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md) 와의 hello 구조는 [ARM 템플릿을](../resource-group-authoring-templates.md) 및 솔루션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="cde52-114">Log Analytics 작업 영역</span><span class="sxs-lookup"><span data-stu-id="cde52-114">Log Analytics Workspace</span></span>
<span data-ttu-id="cde52-115">Log Analytics의 모든 리소스는 [작업 영역](../log-analytics/log-analytics-manage-access.md)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="cde52-116">에 설명 된 대로 [OMS 작업 영역 및 자동화 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello 작업 영역 hello 관리 솔루션에 포함 되어 있지 않지만 hello 솔루션을 설치 하기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="cde52-117">사용할 수 없으면 hello 솔루션 설치 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="cde52-118">hello 이름이 hello 작업 영역의 각 로그 분석 리소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="cde52-119">Hello 사용 하 여 hello 솔루션에서 이렇게 **작업 영역** hello 다음 savedsearch 리소스의 예제에서와 같이 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="cde52-120">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="cde52-120">Saved Searches</span></span>
<span data-ttu-id="cde52-121">포함 [저장 된 검색](../log-analytics/log-analytics-log-searches.md) 솔루션 tooallow 사용자 tooquery 데이터 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="cde52-122">저장 된 검색 아래에 표시 될 **즐겨찾기** hello OMS 포털에서 및 **저장 된 검색** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="cde52-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="cde52-123">각 경고에도 저장된 검색이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="cde52-124">[로그 분석에 저장 된 검색](../log-analytics/log-analytics-log-searches.md) 리소스 유형의 `Microsoft.OperationalInsights/workspaces/savedSearches` 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="cde52-125">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="cde52-126">각각의 저장된 된 검색의 hello 속성 hello 다음 표에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="cde52-127">속성</span><span class="sxs-lookup"><span data-stu-id="cde52-127">Property</span></span> | <span data-ttu-id="cde52-128">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cde52-129">카테고리</span><span class="sxs-lookup"><span data-stu-id="cde52-129">category</span></span> | <span data-ttu-id="cde52-130">hello 저장 된 검색에 대 한 hello 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-130">hello category for hello saved search.</span></span>  <span data-ttu-id="cde52-131">모든 저장 된 검색에 동일한 솔루션은 종종를 공유 하는 hello 단일 범주 hello 콘솔에서 함께 그룹화 되어 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="cde52-132">displayname</span><span class="sxs-lookup"><span data-stu-id="cde52-132">displayname</span></span> | <span data-ttu-id="cde52-133">Hello에 대 한 이름 toodisplay hello 포털에서 검색을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="cde52-134">쿼리</span><span class="sxs-lookup"><span data-stu-id="cde52-134">query</span></span> | <span data-ttu-id="cde52-135">Toorun를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="cde52-136">JSON으로 해석할 수 없는 문자를 포함 하는 경우 hello 쿼리에서 toouse 이스케이프 문자를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="cde52-137">예를 들어, 쿼리 되었으면 **유형: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, hello 솔루션 파일에 쓸지 **유형: AzureActivity OperationName:\" Microsoft.Compute/virtualMachines/write\"**합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="cde52-138">경고</span><span class="sxs-lookup"><span data-stu-id="cde52-138">Alerts</span></span>
<span data-ttu-id="cde52-139">[Log Analytics 경고](../log-analytics/log-analytics-alerts.md)는 일정한 간격으로 저장된 검색을 실행하는 경고 규칙에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="cde52-140">지정 된 조건과 일치 하는 hello hello 쿼리 결과 경고 레코드 만들어지고 하나 이상의 동작이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="cde52-141">경고 규칙 관리 솔루션에서은 다음 세 가지 서로 다른 리소스 hello 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="cde52-142">**저장된 검색.**</span><span class="sxs-lookup"><span data-stu-id="cde52-142">**Saved search.**</span></span>  <span data-ttu-id="cde52-143">실행 되는 hello 로그 검색을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="cde52-144">여러 경고 규칙이 하나의 저장된 검색을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="cde52-145">**일정.**</span><span class="sxs-lookup"><span data-stu-id="cde52-145">**Schedule.**</span></span>  <span data-ttu-id="cde52-146">얼마나 자주 hello 로그 검색 해야 할 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="cde52-147">각 경고 규칙은 일정을 하나만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="cde52-148">**경고 작업.**</span><span class="sxs-lookup"><span data-stu-id="cde52-148">**Alert action.**</span></span>  <span data-ttu-id="cde52-149">각 경고 규칙의 형식 가진 하나의 작업 리소스 갖습니다 **경고** hello 경고 경고 레코드 생성 되 고 경고의 심각도 hello 시기에 대 한 hello 조건 등의 hello 세부 정보를 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="cde52-150">hello 동작 리소스에서 필요에 따라 메일 및 runbook 응답을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="cde52-151">**웹후크 작업(선택 사항).**</span><span class="sxs-lookup"><span data-stu-id="cde52-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="cde52-152">Hello 경고 규칙은 여 webhook을 사용할지를 호출 하는 경우 프로그램의 추가적인 동작이 리소스 형식의 필요 **Webhook**합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="cde52-153">저장된 검색 리소스는 위에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-153">Saved search resources are described above.</span></span>  <span data-ttu-id="cde52-154">hello 다른 리소스 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="cde52-155">일정 리소스</span><span class="sxs-lookup"><span data-stu-id="cde52-155">Schedule resource</span></span>

<span data-ttu-id="cde52-156">저장된 검색은 하나 이상의 일정을 가질 수 있으며 각 일정은 별도의 경고 규칙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="cde52-157">hello 일정 정의 얼마나 자주 hello 검색 실행 되 고 있는 hello를 통해 데이터를 검색 하는 시간 간격을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="cde52-158">일정 리소스 유형의 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="cde52-159">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="cde52-160">다음 표에 hello 일정 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="cde52-161">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-161">Element name</span></span> | <span data-ttu-id="cde52-162">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-162">Required</span></span> | <span data-ttu-id="cde52-163">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-164">사용</span><span class="sxs-lookup"><span data-stu-id="cde52-164">enabled</span></span>       | <span data-ttu-id="cde52-165">예</span><span class="sxs-lookup"><span data-stu-id="cde52-165">Yes</span></span> | <span data-ttu-id="cde52-166">Hello 경고가 생성 될 때 사용 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="cde52-167">interval</span><span class="sxs-lookup"><span data-stu-id="cde52-167">interval</span></span>      | <span data-ttu-id="cde52-168">예</span><span class="sxs-lookup"><span data-stu-id="cde52-168">Yes</span></span> | <span data-ttu-id="cde52-169">Hello 쿼리를 실행 빈도 (분)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="cde52-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="cde52-170">queryTimeSpan</span></span> | <span data-ttu-id="cde52-171">예</span><span class="sxs-lookup"><span data-stu-id="cde52-171">Yes</span></span> | <span data-ttu-id="cde52-172">시간 (분)는 tooevaluate 결과 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="cde52-173">hello 일정 리소스 hello hello 일정 전에 만들어질 수 있도록 저장 된 검색에 의존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="cde52-174">작업</span><span class="sxs-lookup"><span data-stu-id="cde52-174">Actions</span></span>
<span data-ttu-id="cde52-175">Hello로 지정 된 작업 리소스의 두 가지 **형식** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="cde52-176">일정에 따라 하나 필요로 **경고** hello 경고 규칙 및 경고를 만들 때 수행 되는 작업의 hello 세부 정보를 정의 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="cde52-177">포함 될 수도 있습니다는 **Webhook** hello 경고에서 여 webhook을 사용할지를 호출 해야 하는 경우 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="cde52-178">작업 리소스의 형식은 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="cde52-179">경고 작업</span><span class="sxs-lookup"><span data-stu-id="cde52-179">Alert actions</span></span>

<span data-ttu-id="cde52-180">모든 일정은 하나의 **경고** 작업을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="cde52-181">이 hello 경고 및 알림 및 업데이트 관리 작업을 필요에 따라 hello 세부 정보를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="cde52-182">알림을 보내는 전자 메일 tooone 또는 더 많은 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="cde52-183">업데이트 관리 tooattempt tooremediate hello 검색 문제 Azure 자동화에서에서 runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="cde52-184">경고 작업은 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="cde52-185">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="cde52-186">다음 표에서 hello 경고 작업 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="cde52-187">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-187">Element name</span></span> | <span data-ttu-id="cde52-188">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-188">Required</span></span> | <span data-ttu-id="cde52-189">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-190">유형</span><span class="sxs-lookup"><span data-stu-id="cde52-190">Type</span></span> | <span data-ttu-id="cde52-191">예</span><span class="sxs-lookup"><span data-stu-id="cde52-191">Yes</span></span> | <span data-ttu-id="cde52-192">Hello 작업 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-192">Type of hello action.</span></span>  <span data-ttu-id="cde52-193">경고 작업의 **경고**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="cde52-194">이름</span><span class="sxs-lookup"><span data-stu-id="cde52-194">Name</span></span> | <span data-ttu-id="cde52-195">예</span><span class="sxs-lookup"><span data-stu-id="cde52-195">Yes</span></span> | <span data-ttu-id="cde52-196">Hello 경고에 대 한 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-196">Display name for hello alert.</span></span>  <span data-ttu-id="cde52-197">Hello 경고 규칙에 대 한 hello 콘솔에 표시 되는 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="cde52-198">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-198">Description</span></span> | <span data-ttu-id="cde52-199">아니요</span><span class="sxs-lookup"><span data-stu-id="cde52-199">No</span></span> | <span data-ttu-id="cde52-200">Hello 경고의 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="cde52-201">심각도</span><span class="sxs-lookup"><span data-stu-id="cde52-201">Severity</span></span> | <span data-ttu-id="cde52-202">예</span><span class="sxs-lookup"><span data-stu-id="cde52-202">Yes</span></span> | <span data-ttu-id="cde52-203">다음 값에는 hello에서 hello 경고 레코드의 심각도:</span><span class="sxs-lookup"><span data-stu-id="cde52-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="cde52-204">**중요**</span><span class="sxs-lookup"><span data-stu-id="cde52-204">**Critical**</span></span><br><span data-ttu-id="cde52-205">**Warning**</span><span class="sxs-lookup"><span data-stu-id="cde52-205">**Warning**</span></span><br><span data-ttu-id="cde52-206">**정보 제공**</span><span class="sxs-lookup"><span data-stu-id="cde52-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="cde52-207">임계값</span><span class="sxs-lookup"><span data-stu-id="cde52-207">Threshold</span></span>
<span data-ttu-id="cde52-208">이 섹션은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-208">This section is required.</span></span>  <span data-ttu-id="cde52-209">Hello 경고 임계값에 대 한 hello 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="cde52-210">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-210">Element name</span></span> | <span data-ttu-id="cde52-211">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-211">Required</span></span> | <span data-ttu-id="cde52-212">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-213">연산자</span><span class="sxs-lookup"><span data-stu-id="cde52-213">Operator</span></span> | <span data-ttu-id="cde52-214">예</span><span class="sxs-lookup"><span data-stu-id="cde52-214">Yes</span></span> | <span data-ttu-id="cde52-215">다음 값에는 hello에서 hello 비교 연산자:</span><span class="sxs-lookup"><span data-stu-id="cde52-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="cde52-216">**gt = 보다 큼<br>lt = 보다 작음**</span><span class="sxs-lookup"><span data-stu-id="cde52-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="cde52-217">값</span><span class="sxs-lookup"><span data-stu-id="cde52-217">Value</span></span> | <span data-ttu-id="cde52-218">예</span><span class="sxs-lookup"><span data-stu-id="cde52-218">Yes</span></span> | <span data-ttu-id="cde52-219">hello toocompare hello 결과 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="cde52-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="cde52-220">MetricsTrigger</span></span>
<span data-ttu-id="cde52-221">이 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-221">This section is optional.</span></span>  <span data-ttu-id="cde52-222">미터법 경고에는 이 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="cde52-223">미터법 알림은 현재 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="cde52-224">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-224">Element name</span></span> | <span data-ttu-id="cde52-225">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-225">Required</span></span> | <span data-ttu-id="cde52-226">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="cde52-227">TriggerCondition</span></span> | <span data-ttu-id="cde52-228">예</span><span class="sxs-lookup"><span data-stu-id="cde52-228">Yes</span></span> | <span data-ttu-id="cde52-229">Hello 임계값 위반이 나 다음 값에는 hello에서 연속 된 위반의 총 용인지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="cde52-230">**총<br>연속**</span><span class="sxs-lookup"><span data-stu-id="cde52-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="cde52-231">연산자</span><span class="sxs-lookup"><span data-stu-id="cde52-231">Operator</span></span> | <span data-ttu-id="cde52-232">예</span><span class="sxs-lookup"><span data-stu-id="cde52-232">Yes</span></span> | <span data-ttu-id="cde52-233">다음 값에는 hello에서 hello 비교 연산자:</span><span class="sxs-lookup"><span data-stu-id="cde52-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="cde52-234">**gt = 보다 큼<br>lt = 보다 작음**</span><span class="sxs-lookup"><span data-stu-id="cde52-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="cde52-235">값</span><span class="sxs-lookup"><span data-stu-id="cde52-235">Value</span></span> | <span data-ttu-id="cde52-236">예</span><span class="sxs-lookup"><span data-stu-id="cde52-236">Yes</span></span> | <span data-ttu-id="cde52-237">Hello hello 기준 시간 수가 met tootrigger hello 경고 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="cde52-238">제한</span><span class="sxs-lookup"><span data-stu-id="cde52-238">Throttling</span></span>
<span data-ttu-id="cde52-239">이 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-239">This section is optional.</span></span>  <span data-ttu-id="cde52-240">잠시 후 경고가 만들어지고에 대 한 규칙이 동일한 hello에서 toosuppress 경고를 발생 시킬 경우에이 섹션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="cde52-241">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-241">Element name</span></span> | <span data-ttu-id="cde52-242">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-242">Required</span></span> | <span data-ttu-id="cde52-243">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="cde52-244">DurationInMinutes</span></span> | <span data-ttu-id="cde52-245">제한 요소가 포함된 경우 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-245">Yes if Throttling element included</span></span> | <span data-ttu-id="cde52-246">동일한 경고 규칙을 만들면 hello에서 후 분 toosuppress 경고 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="cde52-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="cde52-247">EmailNotification</span></span>
 <span data-ttu-id="cde52-248">이 섹션은 경고 toosend 메일 tooone 또는 더 많은 수신자 hello 하려면 선택적 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="cde52-249">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-249">Element name</span></span> | <span data-ttu-id="cde52-250">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-250">Required</span></span> | <span data-ttu-id="cde52-251">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-252">받는 사람</span><span class="sxs-lookup"><span data-stu-id="cde52-252">Recipients</span></span> | <span data-ttu-id="cde52-253">예</span><span class="sxs-lookup"><span data-stu-id="cde52-253">Yes</span></span> | <span data-ttu-id="cde52-254">전자 메일의 쉼표로 구분 된 목록 hello 다음 예제에서에서와 같은 경고를 만들 때 toosend 알림을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="cde52-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="cde52-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="cde52-256">제목</span><span class="sxs-lookup"><span data-stu-id="cde52-256">Subject</span></span> | <span data-ttu-id="cde52-257">예</span><span class="sxs-lookup"><span data-stu-id="cde52-257">Yes</span></span> | <span data-ttu-id="cde52-258">Hello 메일의 제목 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="cde52-259">첨부 파일</span><span class="sxs-lookup"><span data-stu-id="cde52-259">Attachment</span></span> | <span data-ttu-id="cde52-260">아니요</span><span class="sxs-lookup"><span data-stu-id="cde52-260">No</span></span> | <span data-ttu-id="cde52-261">첨부 파일은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="cde52-262">이 요소를 포함하는 경우 **없음**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="cde52-263">재구성</span><span class="sxs-lookup"><span data-stu-id="cde52-263">Remediation</span></span>
<span data-ttu-id="cde52-264">이 섹션은 선택 사항 응답 toohello 경고의 runbook toostart 하려는 경우이 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="cde52-265">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-265">Element name</span></span> | <span data-ttu-id="cde52-266">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-266">Required</span></span> | <span data-ttu-id="cde52-267">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="cde52-268">RunbookName</span></span> | <span data-ttu-id="cde52-269">예</span><span class="sxs-lookup"><span data-stu-id="cde52-269">Yes</span></span> | <span data-ttu-id="cde52-270">Hello runbook toostart의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="cde52-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="cde52-271">WebhookUri</span></span> | <span data-ttu-id="cde52-272">예</span><span class="sxs-lookup"><span data-stu-id="cde52-272">Yes</span></span> | <span data-ttu-id="cde52-273">Hello runbook에 대 한 hello webhook의 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="cde52-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="cde52-274">Expiry</span></span> | <span data-ttu-id="cde52-275">아니요</span><span class="sxs-lookup"><span data-stu-id="cde52-275">No</span></span> | <span data-ttu-id="cde52-276">Hello 수정 된 날짜와 시간에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="cde52-277">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="cde52-277">Webhook actions</span></span>

<span data-ttu-id="cde52-278">Webhook 작업 URL을 호출 하 여 선택적으로 전송 되는 페이로드 toobe 제공 하는 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="cde52-279">Azure 자동화 runbook 이외의 프로세스를 호출할 수 있는 webhook에 대 한 보관 점을 제외 하 고 서로 유사한 tooRemediation 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="cde52-280">또한 hello 페이로드 배달 toobe toohello 원격 프로세스를 제공 하는 중 추가 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="cde52-281">결제 경고가 됩니다 여 webhook을 사용할지를 호출 하는 경우의 형식과 동작 리소스는 필요 **Webhook** 더하기 toohello에 **경고** 작업 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="cde52-282">다음 표에서 hello Webhook 작업 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="cde52-283">요소 이름</span><span class="sxs-lookup"><span data-stu-id="cde52-283">Element name</span></span> | <span data-ttu-id="cde52-284">필수</span><span class="sxs-lookup"><span data-stu-id="cde52-284">Required</span></span> | <span data-ttu-id="cde52-285">설명</span><span class="sxs-lookup"><span data-stu-id="cde52-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="cde52-286">type</span><span class="sxs-lookup"><span data-stu-id="cde52-286">type</span></span> | <span data-ttu-id="cde52-287">예</span><span class="sxs-lookup"><span data-stu-id="cde52-287">Yes</span></span> | <span data-ttu-id="cde52-288">Hello 작업 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-288">Type of hello action.</span></span>  <span data-ttu-id="cde52-289">웹후크 작업의 **웹후크**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="cde52-290">name</span><span class="sxs-lookup"><span data-stu-id="cde52-290">name</span></span> | <span data-ttu-id="cde52-291">예</span><span class="sxs-lookup"><span data-stu-id="cde52-291">Yes</span></span> | <span data-ttu-id="cde52-292">Hello 동작에 대 한 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-292">Display name for hello action.</span></span>  <span data-ttu-id="cde52-293">Hello 콘솔에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="cde52-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="cde52-294">wehookUri</span></span> | <span data-ttu-id="cde52-295">예</span><span class="sxs-lookup"><span data-stu-id="cde52-295">Yes</span></span> | <span data-ttu-id="cde52-296">Hello webhook에 대 한 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="cde52-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="cde52-297">customPayload</span></span> | <span data-ttu-id="cde52-298">아니요</span><span class="sxs-lookup"><span data-stu-id="cde52-298">No</span></span> | <span data-ttu-id="cde52-299">사용자 지정 페이로드 toobe toohello webhook을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="cde52-300">hello 형식 어떤 hello webhook 예상에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="cde52-301">샘플</span><span class="sxs-lookup"><span data-stu-id="cde52-301">Sample</span></span>

<span data-ttu-id="cde52-302">다음은 hello 다음 리소스를 포함 하는 포함 하는 솔루션의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="cde52-303">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="cde52-303">Saved search</span></span>
- <span data-ttu-id="cde52-304">일정</span><span class="sxs-lookup"><span data-stu-id="cde52-304">Schedule</span></span>
- <span data-ttu-id="cde52-305">경고 작업</span><span class="sxs-lookup"><span data-stu-id="cde52-305">Alert action</span></span>
- <span data-ttu-id="cde52-306">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="cde52-306">Webhook action</span></span>

<span data-ttu-id="cde52-307">샘플 사용 하 여 hello [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 와 솔루션에 일반적으로 사용 되는 변수 hello 리소스 정의에서 toohardcoding 값을 반대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="cde52-308">다음 매개 변수 파일 hello이이 솔루션에 대 한 샘플 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="cde52-309">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cde52-309">Next steps</span></span>
* <span data-ttu-id="cde52-310">[뷰 추가](operations-management-suite-solutions-resources-views.md) tooyour 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="cde52-311">[자동화 runbook 및 기타 리소스를 추가](operations-management-suite-solutions-resources-automation.md) tooyour 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="cde52-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>


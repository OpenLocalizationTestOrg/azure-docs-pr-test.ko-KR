---
title: "OMS 솔루션에 저장된 검색 및 경고 | Microsoft Docs"
description: "OMS의 솔루션은 일반적으로 솔루션에서 수집한 데이터를 분석하기 위해 Log Analytics에 저장된 검색을 포함하게 됩니다.  또한 중요한 문제에 대한 응답으로 사용자에게 알리거나 자동으로 조치를 취하기 위한 경고를 정의합니다.  이 문서에서는 관리 솔루션에 포함되도록 ARM 템플릿에서 Log Analytics 저장된 검색 및 경고를 정의하는 방법을 설명합니다."
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
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="ff217-105">OMS 관리 솔루션(미리 보기)에 Log Analytics에서 저장한 검색 및 경고 추가</span><span class="sxs-lookup"><span data-stu-id="ff217-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="ff217-106">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="ff217-107">아래 설명된 스키마는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="ff217-108">[OMS의 관리 솔루션](operations-management-suite-solutions.md)은 일반적으로 솔루션에서 수집한 데이터를 분석하기 위해 Log Analytics에 [저장된 검색](../log-analytics/log-analytics-log-searches.md)을 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="ff217-109">또한 중요한 문제에 대한 응답으로 사용자에게 알리거나 자동으로 조치를 취하기 위한 [경고](../log-analytics/log-analytics-alerts.md)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="ff217-110">이 문서에서는 [관리 솔루션](operations-management-suite-solutions-creating.md)에 포함되도록 [리소스 관리 템플릿](../resource-manager-template-walkthrough.md)에서 Log Analytics 저장된 검색 및 경고를 정의하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ff217-111">이 문서의 샘플에는 관리 솔루션에 필요하거나 공통적이며 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)에서 설명한 매개 변수와 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ff217-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ff217-112">Prerequisites</span></span>
<span data-ttu-id="ff217-113">이 문서에서는 여러분이 [관리 솔루션을 만드는 방법](operations-management-suite-solutions-creating.md)과 [ARM 템플릿](../resource-group-authoring-templates.md) 및 솔루션 파일의 구조를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="ff217-114">Log Analytics 작업 영역</span><span class="sxs-lookup"><span data-stu-id="ff217-114">Log Analytics Workspace</span></span>
<span data-ttu-id="ff217-115">Log Analytics의 모든 리소스는 [작업 영역](../log-analytics/log-analytics-manage-access.md)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="ff217-116">[OMS 작업 영역 및 Automation 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account)에서 설명한 대로 작업 영역은 관리 솔루션에 포함되지 않지만, 솔루션이 설치되기 전에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="ff217-117">계정을 사용할 수 없으면 솔루션 설치에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="ff217-118">작업 영역 이름은 각 Log Analytics 리소스의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="ff217-119">이 작업은 다음 저장된 검색 리소스 예제와 같이 **workspace** 매개 변수가 포함된 솔루션에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="ff217-120">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="ff217-120">Saved Searches</span></span>
<span data-ttu-id="ff217-121">솔루션에서 수집한 데이터를 사용자가 쿼리할 수 있도록 솔루션에 [저장된 검색](../log-analytics/log-analytics-log-searches.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="ff217-122">저장된 검색은 OMS 포털의 **즐겨찾기**와 Azure Portal의 **저장된 검색**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="ff217-123">각 경고에도 저장된 검색이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="ff217-124">[Log Analytics 및 저장된 검색](../log-analytics/log-analytics-log-searches.md) 리소스는 `Microsoft.OperationalInsights/workspaces/savedSearches` 형식을 가지며 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="ff217-125">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="ff217-126">저장된 검색의 각 속성은 다음 테이블에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="ff217-127">속성</span><span class="sxs-lookup"><span data-stu-id="ff217-127">Property</span></span> | <span data-ttu-id="ff217-128">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ff217-129">카테고리</span><span class="sxs-lookup"><span data-stu-id="ff217-129">category</span></span> | <span data-ttu-id="ff217-130">저장된 검색의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-130">The category for the saved search.</span></span>  <span data-ttu-id="ff217-131">같은 솔루션에 있는 저장된 검색은 종종 단일 범주를 공유하므로 콘솔에서 함께 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="ff217-132">displayname</span><span class="sxs-lookup"><span data-stu-id="ff217-132">displayname</span></span> | <span data-ttu-id="ff217-133">포털에서 저장된 검색에 표시할 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="ff217-134">쿼리</span><span class="sxs-lookup"><span data-stu-id="ff217-134">query</span></span> | <span data-ttu-id="ff217-135">실행할 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="ff217-136">JSON으로 해석될 수 있는 문자를 포함하고 있는 경우 쿼리에 이스케이프 문자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="ff217-137">예를 들어 쿼리가 **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**이면 솔루션 파일에 **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**라고 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="ff217-138">경고</span><span class="sxs-lookup"><span data-stu-id="ff217-138">Alerts</span></span>
<span data-ttu-id="ff217-139">[Log Analytics 경고](../log-analytics/log-analytics-alerts.md)는 일정한 간격으로 저장된 검색을 실행하는 경고 규칙에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="ff217-140">쿼리 결과가 지정된 기준과 일치하면 경고 레코드가 생성되고 하나 이상의 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="ff217-141">관리 솔루션의 경고 규칙은 다음 세 가지 리소스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="ff217-142">**저장된 검색.**</span><span class="sxs-lookup"><span data-stu-id="ff217-142">**Saved search.**</span></span>  <span data-ttu-id="ff217-143">실행될 로그 검색을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="ff217-144">여러 경고 규칙이 하나의 저장된 검색을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="ff217-145">**일정.**</span><span class="sxs-lookup"><span data-stu-id="ff217-145">**Schedule.**</span></span>  <span data-ttu-id="ff217-146">로그 검색이 실행될 빈도를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="ff217-147">각 경고 규칙은 일정을 하나만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="ff217-148">**경고 작업.**</span><span class="sxs-lookup"><span data-stu-id="ff217-148">**Alert action.**</span></span>  <span data-ttu-id="ff217-149">각 경고 규칙은 경고 레코드가 생성되는 시기, 경고 심각도 등의 경고 세부 정보를 정의하는 **경고** 형식의 작업 리소스 하나를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="ff217-150">작업 리소스는 메일 및 runbook 응답을 선택적으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="ff217-151">**웹후크 작업(선택 사항).**</span><span class="sxs-lookup"><span data-stu-id="ff217-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="ff217-152">경고 규칙이 웹후크를 호출하면 **웹후크** 형식의 추가 작업 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="ff217-153">저장된 검색 리소스는 위에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-153">Saved search resources are described above.</span></span>  <span data-ttu-id="ff217-154">다른 리소스는 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="ff217-155">일정 리소스</span><span class="sxs-lookup"><span data-stu-id="ff217-155">Schedule resource</span></span>

<span data-ttu-id="ff217-156">저장된 검색은 하나 이상의 일정을 가질 수 있으며 각 일정은 별도의 경고 규칙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="ff217-157">일정은 검색이 실행되는 빈도 및 데이터가 검색되는 시간 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="ff217-158">일정 리소스는 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` 형식을 가지며 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="ff217-159">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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



<span data-ttu-id="ff217-160">일정 리소스의 속성은 다음 테이블에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="ff217-161">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-161">Element name</span></span> | <span data-ttu-id="ff217-162">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-162">Required</span></span> | <span data-ttu-id="ff217-163">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-164">사용</span><span class="sxs-lookup"><span data-stu-id="ff217-164">enabled</span></span>       | <span data-ttu-id="ff217-165">예</span><span class="sxs-lookup"><span data-stu-id="ff217-165">Yes</span></span> | <span data-ttu-id="ff217-166">경고를 만들 때 사용 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="ff217-167">interval</span><span class="sxs-lookup"><span data-stu-id="ff217-167">interval</span></span>      | <span data-ttu-id="ff217-168">예</span><span class="sxs-lookup"><span data-stu-id="ff217-168">Yes</span></span> | <span data-ttu-id="ff217-169">쿼리가 실행되는 빈도(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="ff217-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="ff217-170">queryTimeSpan</span></span> | <span data-ttu-id="ff217-171">예</span><span class="sxs-lookup"><span data-stu-id="ff217-171">Yes</span></span> | <span data-ttu-id="ff217-172">결과를 평가하는 시간의 길이(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="ff217-173">일정 전에 저장된 검색이 생성되도록 일정 리소스는 저장된 검색에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="ff217-174">작업</span><span class="sxs-lookup"><span data-stu-id="ff217-174">Actions</span></span>
<span data-ttu-id="ff217-175">**Type** 속성에서 지정하는 두 가지 형식의 작업 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="ff217-176">일정에는 경고 규칙 세부 정보 그리고 경고가 생성될 때 수행할 작업을 정의하는 **경고** 작업 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="ff217-177">또한 경고에서 웹후크를 호출해야 하는 경우 **웹후크** 작업을 포함해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="ff217-178">작업 리소스의 형식은 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="ff217-179">경고 작업</span><span class="sxs-lookup"><span data-stu-id="ff217-179">Alert actions</span></span>

<span data-ttu-id="ff217-180">모든 일정은 하나의 **경고** 작업을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="ff217-181">이 경고 작업은 경고의 세부 정보를 정의하고 필요에 따라 알림 및 재구성 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="ff217-182">알림은 하나 이상의 주소에 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="ff217-183">재구성은 Azure Automation에서 runbook을 시작하여 검색된 문제 해결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="ff217-184">경고 작업의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="ff217-185">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



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

<span data-ttu-id="ff217-186">경고 작업 리소스의 속성은 다음 테이블에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="ff217-187">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-187">Element name</span></span> | <span data-ttu-id="ff217-188">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-188">Required</span></span> | <span data-ttu-id="ff217-189">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-190">유형</span><span class="sxs-lookup"><span data-stu-id="ff217-190">Type</span></span> | <span data-ttu-id="ff217-191">예</span><span class="sxs-lookup"><span data-stu-id="ff217-191">Yes</span></span> | <span data-ttu-id="ff217-192">작업의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-192">Type of the action.</span></span>  <span data-ttu-id="ff217-193">경고 작업의 **경고**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="ff217-194">이름</span><span class="sxs-lookup"><span data-stu-id="ff217-194">Name</span></span> | <span data-ttu-id="ff217-195">예</span><span class="sxs-lookup"><span data-stu-id="ff217-195">Yes</span></span> | <span data-ttu-id="ff217-196">경고에 대한 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-196">Display name for the alert.</span></span>  <span data-ttu-id="ff217-197">경고 규칙에 대한 콘솔에 표시되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="ff217-198">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-198">Description</span></span> | <span data-ttu-id="ff217-199">아니요</span><span class="sxs-lookup"><span data-stu-id="ff217-199">No</span></span> | <span data-ttu-id="ff217-200">경고에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="ff217-201">심각도</span><span class="sxs-lookup"><span data-stu-id="ff217-201">Severity</span></span> | <span data-ttu-id="ff217-202">예</span><span class="sxs-lookup"><span data-stu-id="ff217-202">Yes</span></span> | <span data-ttu-id="ff217-203">다음 값의 경고 레코드의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="ff217-204">**중요**</span><span class="sxs-lookup"><span data-stu-id="ff217-204">**Critical**</span></span><br><span data-ttu-id="ff217-205">**Warning**</span><span class="sxs-lookup"><span data-stu-id="ff217-205">**Warning**</span></span><br><span data-ttu-id="ff217-206">**정보 제공**</span><span class="sxs-lookup"><span data-stu-id="ff217-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="ff217-207">임계값</span><span class="sxs-lookup"><span data-stu-id="ff217-207">Threshold</span></span>
<span data-ttu-id="ff217-208">이 섹션은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-208">This section is required.</span></span>  <span data-ttu-id="ff217-209">경고 임계값의 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="ff217-210">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-210">Element name</span></span> | <span data-ttu-id="ff217-211">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-211">Required</span></span> | <span data-ttu-id="ff217-212">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-213">연산자</span><span class="sxs-lookup"><span data-stu-id="ff217-213">Operator</span></span> | <span data-ttu-id="ff217-214">예</span><span class="sxs-lookup"><span data-stu-id="ff217-214">Yes</span></span> | <span data-ttu-id="ff217-215">다음 값의 비교 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="ff217-216">**gt = 보다 큼<br>lt = 보다 작음**</span><span class="sxs-lookup"><span data-stu-id="ff217-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ff217-217">값</span><span class="sxs-lookup"><span data-stu-id="ff217-217">Value</span></span> | <span data-ttu-id="ff217-218">예</span><span class="sxs-lookup"><span data-stu-id="ff217-218">Yes</span></span> | <span data-ttu-id="ff217-219">결과를 비교하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="ff217-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="ff217-220">MetricsTrigger</span></span>
<span data-ttu-id="ff217-221">이 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-221">This section is optional.</span></span>  <span data-ttu-id="ff217-222">미터법 경고에는 이 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ff217-223">미터법 알림은 현재 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="ff217-224">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-224">Element name</span></span> | <span data-ttu-id="ff217-225">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-225">Required</span></span> | <span data-ttu-id="ff217-226">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="ff217-227">TriggerCondition</span></span> | <span data-ttu-id="ff217-228">예</span><span class="sxs-lookup"><span data-stu-id="ff217-228">Yes</span></span> | <span data-ttu-id="ff217-229">임계값이 총 위반 수인지 아니면 연속 위반인지 다음 값을 사용하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="ff217-230">**총<br>연속**</span><span class="sxs-lookup"><span data-stu-id="ff217-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="ff217-231">연산자</span><span class="sxs-lookup"><span data-stu-id="ff217-231">Operator</span></span> | <span data-ttu-id="ff217-232">예</span><span class="sxs-lookup"><span data-stu-id="ff217-232">Yes</span></span> | <span data-ttu-id="ff217-233">다음 값의 비교 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="ff217-234">**gt = 보다 큼<br>lt = 보다 작음**</span><span class="sxs-lookup"><span data-stu-id="ff217-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ff217-235">값</span><span class="sxs-lookup"><span data-stu-id="ff217-235">Value</span></span> | <span data-ttu-id="ff217-236">예</span><span class="sxs-lookup"><span data-stu-id="ff217-236">Yes</span></span> | <span data-ttu-id="ff217-237">경고를 트리거하기 위해 조건을 충족해야 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="ff217-238">제한</span><span class="sxs-lookup"><span data-stu-id="ff217-238">Throttling</span></span>
<span data-ttu-id="ff217-239">이 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-239">This section is optional.</span></span>  <span data-ttu-id="ff217-240">경고가 생성된 후 일정 시간 동안 같은 규칙의 경고를 표시하지 않으려면 이 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="ff217-241">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-241">Element name</span></span> | <span data-ttu-id="ff217-242">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-242">Required</span></span> | <span data-ttu-id="ff217-243">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="ff217-244">DurationInMinutes</span></span> | <span data-ttu-id="ff217-245">제한 요소가 포함된 경우 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-245">Yes if Throttling element included</span></span> | <span data-ttu-id="ff217-246">같은 경고 규칙에서 경고가 생성되면 이 시간 동안 경고를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="ff217-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="ff217-247">EmailNotification</span></span>
 <span data-ttu-id="ff217-248">이 섹션은 선택 사항입니다. 한 명 이상의 수신자에게 메일을 보내 경고하려면 이 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="ff217-249">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-249">Element name</span></span> | <span data-ttu-id="ff217-250">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-250">Required</span></span> | <span data-ttu-id="ff217-251">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-252">받는 사람</span><span class="sxs-lookup"><span data-stu-id="ff217-252">Recipients</span></span> | <span data-ttu-id="ff217-253">예</span><span class="sxs-lookup"><span data-stu-id="ff217-253">Yes</span></span> | <span data-ttu-id="ff217-254">다음 예제와 같이 경고가 생성되면 알림을 보낼 쉼표로 구분된 전자 메일 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="ff217-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="ff217-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="ff217-256">제목</span><span class="sxs-lookup"><span data-stu-id="ff217-256">Subject</span></span> | <span data-ttu-id="ff217-257">예</span><span class="sxs-lookup"><span data-stu-id="ff217-257">Yes</span></span> | <span data-ttu-id="ff217-258">메일의 제목 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="ff217-259">첨부 파일</span><span class="sxs-lookup"><span data-stu-id="ff217-259">Attachment</span></span> | <span data-ttu-id="ff217-260">아니요</span><span class="sxs-lookup"><span data-stu-id="ff217-260">No</span></span> | <span data-ttu-id="ff217-261">첨부 파일은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="ff217-262">이 요소를 포함하는 경우 **없음**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="ff217-263">재구성</span><span class="sxs-lookup"><span data-stu-id="ff217-263">Remediation</span></span>
<span data-ttu-id="ff217-264">이 섹션은 선택 사항입니다. 경고에 대한 응답으로 runbook을 시작하려면 이 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="ff217-265">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-265">Element name</span></span> | <span data-ttu-id="ff217-266">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-266">Required</span></span> | <span data-ttu-id="ff217-267">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="ff217-268">RunbookName</span></span> | <span data-ttu-id="ff217-269">예</span><span class="sxs-lookup"><span data-stu-id="ff217-269">Yes</span></span> | <span data-ttu-id="ff217-270">시작할 runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="ff217-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="ff217-271">WebhookUri</span></span> | <span data-ttu-id="ff217-272">예</span><span class="sxs-lookup"><span data-stu-id="ff217-272">Yes</span></span> | <span data-ttu-id="ff217-273">runbook의 웹후크 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="ff217-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="ff217-274">Expiry</span></span> | <span data-ttu-id="ff217-275">아니요</span><span class="sxs-lookup"><span data-stu-id="ff217-275">No</span></span> | <span data-ttu-id="ff217-276">재구성이 만료되는 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="ff217-277">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="ff217-277">Webhook actions</span></span>

<span data-ttu-id="ff217-278">웹후크 작업은 URL을 호출하고 선택적으로 보낼 페이로드를 제공하는 것으로 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="ff217-279">이들은 웹후크에 대해 Azure 자동화 Runbook 이외의 프로세스를 호출할 수 있다는 것을 제외하고 수정 작업과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="ff217-280">또한 원격 프로세스에 전달할 페이로드를 제공하는 추가 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="ff217-281">경고에서 웹후크를 호출하는 경우 **경고** 작업 리소스 외에도 **웹후크** 형식의 작업 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

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

<span data-ttu-id="ff217-282">웹후크 작업 리소스의 속성은 다음 표에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="ff217-283">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ff217-283">Element name</span></span> | <span data-ttu-id="ff217-284">필수</span><span class="sxs-lookup"><span data-stu-id="ff217-284">Required</span></span> | <span data-ttu-id="ff217-285">설명</span><span class="sxs-lookup"><span data-stu-id="ff217-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ff217-286">type</span><span class="sxs-lookup"><span data-stu-id="ff217-286">type</span></span> | <span data-ttu-id="ff217-287">예</span><span class="sxs-lookup"><span data-stu-id="ff217-287">Yes</span></span> | <span data-ttu-id="ff217-288">작업의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-288">Type of the action.</span></span>  <span data-ttu-id="ff217-289">웹후크 작업의 **웹후크**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="ff217-290">name</span><span class="sxs-lookup"><span data-stu-id="ff217-290">name</span></span> | <span data-ttu-id="ff217-291">예</span><span class="sxs-lookup"><span data-stu-id="ff217-291">Yes</span></span> | <span data-ttu-id="ff217-292">작업의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-292">Display name for the action.</span></span>  <span data-ttu-id="ff217-293">콘솔에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="ff217-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="ff217-294">wehookUri</span></span> | <span data-ttu-id="ff217-295">예</span><span class="sxs-lookup"><span data-stu-id="ff217-295">Yes</span></span> | <span data-ttu-id="ff217-296">웹후크의 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="ff217-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="ff217-297">customPayload</span></span> | <span data-ttu-id="ff217-298">아니요</span><span class="sxs-lookup"><span data-stu-id="ff217-298">No</span></span> | <span data-ttu-id="ff217-299">웹후크에 보낼 사용자 지정 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="ff217-300">형식은 예상하는 웹후크에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="ff217-301">샘플</span><span class="sxs-lookup"><span data-stu-id="ff217-301">Sample</span></span>

<span data-ttu-id="ff217-302">다음은 다음 리소스를 포함하는 솔루션의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="ff217-303">저장된 검색</span><span class="sxs-lookup"><span data-stu-id="ff217-303">Saved search</span></span>
- <span data-ttu-id="ff217-304">일정</span><span class="sxs-lookup"><span data-stu-id="ff217-304">Schedule</span></span>
- <span data-ttu-id="ff217-305">경고 작업</span><span class="sxs-lookup"><span data-stu-id="ff217-305">Alert action</span></span>
- <span data-ttu-id="ff217-306">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="ff217-306">Webhook action</span></span>

<span data-ttu-id="ff217-307">이 샘플에서는 리소스 정의의 값을 하드 코딩하는 대신 솔루션에 일반적으로 사용되는 [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

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
              "Description": "List of recipients for the email alert separated by semicolon"
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


<span data-ttu-id="ff217-308">다음 매개 변수 파일은 이 솔루션에 대한 샘플 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-308">The following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="ff217-309">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff217-309">Next steps</span></span>
* <span data-ttu-id="ff217-310">관리 솔루션에 대한 [보기를 추가](operations-management-suite-solutions-resources-views.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="ff217-311">관리 솔루션에 [Automation runbook 및 기타 리소스를 추가](operations-management-suite-solutions-resources-automation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff217-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>


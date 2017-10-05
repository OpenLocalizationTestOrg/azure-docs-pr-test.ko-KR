---
title: "OMS의 솔루션 대상 지정 | Microsoft Docs"
description: "솔루션 대상 지정은 관리 솔루션을 특정 에이전트 집합으로 제한할 수 있도록 하는 OMS(Operations Management Suite)의 기능입니다.  이 문서에서는 범위 구성을 만들고 솔루션에 적용하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: cb73a2d7ae57a5a11869259dbe913ae83ffb2b01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-to-scope-management-solutions-to-specific-agents-preview"></a><span data-ttu-id="36bd4-104">OMS(Operations Management Suite)의 솔루션 대상 지정 기능을 사용하여 관리 솔루션의 범위를 특정 에이전트(미리 보기)로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-104">Use solution targeting in Operations Management Suite (OMS) to scope management solutions to specific agents (Preview)</span></span>
<span data-ttu-id="36bd4-105">OMS에 솔루션을 추가하면 기본적으로 Log Analytics 작업 영역에 연결된 모든 Windows 및 Linux 에이전트에 의해 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-105">When you add a solution to OMS, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span></span>  <span data-ttu-id="36bd4-106">특정 에이전트 집합으로 제한하여 비용을 관리하고 솔루션에 대해 수집되는 데이터 양을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-106">You may want to manage your costs and limit the amount of data collected for a solution by limiting it to a particular set of agents.</span></span>  <span data-ttu-id="36bd4-107">이 문서에서는 솔루션에 범위를 적용할 수 있는 OMS 기능인 **솔루션 대상 지정**을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-107">This article describes how to use **Solution Targeting** which is an OMS feature that allows you to apply a scope to your solutions.</span></span>

## <a name="how-to-target-a-solution"></a><span data-ttu-id="36bd4-108">솔루션 대상 지정 방법</span><span class="sxs-lookup"><span data-stu-id="36bd4-108">How to target a solution</span></span>
<span data-ttu-id="36bd4-109">솔루션 대상 지정은 다음 섹션에 설명된 것처럼 3단계로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-109">There are three steps to targeting a solution as described in the following sections.</span></span>  <span data-ttu-id="36bd4-110">OMS 포털 및 Azure Portal은 세 가지 단계에 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-110">Note that you will need both the OMS portal and the Azure portal for different steps.</span></span>


### <a name="1-create-a-computer-group"></a><span data-ttu-id="36bd4-111">1. 컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="36bd4-111">1. Create a computer group</span></span>
<span data-ttu-id="36bd4-112">Log Analytics에서 [컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md)을 만들어 범위에 포함하려는 컴퓨터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-112">You specify the computers that you want to include in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span></span>  <span data-ttu-id="36bd4-113">컴퓨터 그룹은 로그 검색을 기준으로 하거나 Active Directory 또는 WSUS 그룹 등의 다른 원본에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-113">The computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span></span> <span data-ttu-id="36bd4-114">[아래에 설명된](#solutions-and-agents-that-cant-be-targeted) 것처럼 Log Analytics에 직접 연결된 컴퓨터만 범위에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-114">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected to Log Analytics will be included in the scope.</span></span>

<span data-ttu-id="36bd4-115">작업 영역에서 컴퓨터 그룹을 만든 후에는 하나 이상의 솔루션에 적용될 수 있는 범위 구성에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-115">Once you have the computer group created in your workspace, then you'll include it in a scope configuration that can be applied to one or more solutions.</span></span>
 
 
 ### <a name="2-create-a-scope-configuration"></a><span data-ttu-id="36bd4-116">2. 범위 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="36bd4-116">2. Create a scope configuration</span></span>
 <span data-ttu-id="36bd4-117">**범위 구성**은 하나 이상의 컴퓨터 그룹을 포함하고 하나 이상의 솔루션에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-117">A **Scope Configuration** includes one or more computer groups and can be applied to one or more solutions.</span></span> 
 
 <span data-ttu-id="36bd4-118">다음 프로세스를 사용하여 범위 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-118">Create a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="36bd4-119">Azure Portal에서 **Log Analytics**로 이동한 후 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-119">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="36bd4-120">**작업 영역 데이터 원본** 아래에 있는 작업 영역에 대한 속성에서 **범위 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-120">In the properties for the workspace under **Workspace Data Sources** select **Scope Configurations**.</span></span>
 3. <span data-ttu-id="36bd4-121">**추가**를 클릭하여 새 범위 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-121">Click **Add** to create a new scope configuration.</span></span>
 4. <span data-ttu-id="36bd4-122">범위 구성의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-122">Type a **Name** for the scope configuration.</span></span>
 5. <span data-ttu-id="36bd4-123">**컴퓨터 그룹 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-123">Click **Select Computer Groups**.</span></span>
 6. <span data-ttu-id="36bd4-124">만든 컴퓨터 그룹과 필요에 따라 구성에 추가할 다른 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-124">Select the computer group that you created and optionally any other groups to add to the configuration.</span></span>  <span data-ttu-id="36bd4-125">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-125">Click **Select**.</span></span>  
 6. <span data-ttu-id="36bd4-126">**확인**을 클릭하여 범위 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-126">Click **OK** to create the scope configuration.</span></span> 


 ### <a name="3-apply-the-scope-configuration-to-a-solution"></a><span data-ttu-id="36bd4-127">3. 솔루션에 범위 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-127">3. Apply the scope configuration to a solution.</span></span>
<span data-ttu-id="36bd4-128">범위를 구성했으면 하나 이상의 솔루션에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-128">Once you have a scope configuration, then you can apply it to one or more solutions.</span></span>  <span data-ttu-id="36bd4-129">단일 범위 구성을 여러 솔루션에서 사용할 수 있지만, 각 솔루션은 범위 구성을 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-129">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span></span>

<span data-ttu-id="36bd4-130">다음 프로세스를 사용하여 범위 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-130">Apply a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="36bd4-131">Azure Portal에서 **Log Analytics**로 이동한 후 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-131">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="36bd4-132">작업 영역에 대한 속성에서 **솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-132">In the properties for the workspace select **Solutions**.</span></span>
 3. <span data-ttu-id="36bd4-133">범위를 지정하려는 솔루션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-133">Click on the solution you want to scope.</span></span>
 4. <span data-ttu-id="36bd4-134">**작업 영역 데이터 원본** 아래에 있는 솔루션에 대한 속성에서 **솔루션 범위 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-134">In the properties for the solution under **Workspace Data Sources** select **Solution Targeting**.</span></span>  <span data-ttu-id="36bd4-135">이 옵션을 사용할 수 없으면 [이 솔루션을 대상으로 지정할 수 없습니다](#solutions-and-agents-that-cant-be-targeted).</span><span class="sxs-lookup"><span data-stu-id="36bd4-135">If the option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span></span>
 5. <span data-ttu-id="36bd4-136">**범위 구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-136">Click **Add scope configuration**.</span></span>  <span data-ttu-id="36bd4-137">이 솔루션에 구성이 이미 적용되어 있으면 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-137">If you already have a configuration applied to this solution then this option will be unavailable.</span></span>  <span data-ttu-id="36bd4-138">다른 구성을 추가하기 전에 기존 구성을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-138">You must remove the existing configuration before adding another one.</span></span>
 6. <span data-ttu-id="36bd4-139">만든 범위 구성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-139">Click on the scope configuration that you created.</span></span>
 7. <span data-ttu-id="36bd4-140">구성의 **상태**가 **성공**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-140">Watch the **Status** of the configuration to ensure that it shows **Succeeded**.</span></span>  <span data-ttu-id="36bd4-141">상태 오류가 나타나면 구성 오른쪽에 있는 줄임표를 클릭한 다음 **범위 구성 편집**을 선택하여 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-141">If the status indicates an error, then click the ellipse to the right of the configuration and select **Edit scope configuration** to make changes.</span></span>

## <a name="solutions-and-agents-that-cant-be-targeted"></a><span data-ttu-id="36bd4-142">대상으로 지정할 수 없는 솔루션 및 에이전트</span><span class="sxs-lookup"><span data-stu-id="36bd4-142">Solutions and agents that can't be targeted</span></span>
<span data-ttu-id="36bd4-143">다음은 솔루션 대상 지정에 사용할 수 없는 에이전트 및 솔루션에 대한 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-143">Following are the criteria for agents and solutions that can't be used with solution targeting.</span></span>

- <span data-ttu-id="36bd4-144">솔루션 대상 지정은 에이전트에 배포하는 솔루션에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-144">Solution targeting only applies to solutions that deploy to agents.</span></span>
- <span data-ttu-id="36bd4-145">솔루션 대상 지정은 Microsoft에서 제공하는 솔루션에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-145">Solution targeting only applies to solutions provided by Microsoft.</span></span>  <span data-ttu-id="36bd4-146">[사용자 또는 파트너가 직접 만든](operations-management-suite-solutions-creating.md) 솔루션에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-146">It does not apply to solutions [created by yourself or partners](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="36bd4-147">Log Analytics에 직접 연결되는 에이전트만 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-147">You can only filter out agents that connect directly to Log Analytics.</span></span>  <span data-ttu-id="36bd4-148">솔루션은 범위 구성에 포함되는지 여부에 관계없이 연결된 Operations Manager 관리 그룹의 일부인 모든 에이전트에 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-148">Solutions will automatically deploy to any agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span></span>

### <a name="exceptions"></a><span data-ttu-id="36bd4-149">예외</span><span class="sxs-lookup"><span data-stu-id="36bd4-149">Exceptions</span></span>
<span data-ttu-id="36bd4-150">명시된 조건에 맞더라도 다음 솔루션에는 솔루션 대상 지정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36bd4-150">Solution targeting cannot be used with the following solutions even though they fit the stated criteria.</span></span>

- <span data-ttu-id="36bd4-151">에이전트 상태 평가</span><span class="sxs-lookup"><span data-stu-id="36bd4-151">Agent Health Assessment</span></span>

## <a name="next-steps"></a><span data-ttu-id="36bd4-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36bd4-152">Next steps</span></span>
- <span data-ttu-id="36bd4-153">[작업 영역에 Azure Log Analytics 관리 솔루션 추가](../log-analytics/log-analytics-add-solutions.md)에서 사용 주인 환경에 설치할 수 있는 솔루션을 비롯한 관리 솔루션에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="36bd4-153">Learn more about management solutions including the solutions that are available to install in your environment at [Add Azure Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
- <span data-ttu-id="36bd4-154">[Log Analytics 로그 검색의 컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md)에서 컴퓨터 그룹 생성에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="36bd4-154">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span></span>
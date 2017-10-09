---
title: "OMS의 대상으로 aaaSolution | Microsoft Docs"
description: "솔루션 Targeting는에 OMS Operations Management Suite () toolimit 관리 솔루션 tooa 특정 에이전트 집합을 허용 하는 기능입니다.  이 문서에서는 설명 방법을 toocreate 범위 구성 tooa 솔루션을 적용 합니다."
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
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a><span data-ttu-id="333bb-104">Operations Management Suite (OMS)에서 tooscope 관리 솔루션 toospecific 에이전트 (미리 보기)를 대상으로 하는 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="333bb-104">Use solution targeting in Operations Management Suite (OMS) tooscope management solutions toospecific agents (Preview)</span></span>
<span data-ttu-id="333bb-105">솔루션 tooOMS를 추가 하면 기본 tooall Windows 및 Linux 에이전트 연결된 tooyour 로그 분석 작업 영역에 의해 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-105">When you add a solution tooOMS, it's automatically deployed by default tooall Windows and Linux agents connected tooyour Log Analytics workspace.</span></span>  <span data-ttu-id="333bb-106">Tooa 특정 에이전트 집합을 제한 하 여 솔루션에 대 한 toomanage 프로그램 비용 및 제한 hello 양의 데이터 수집을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-106">You may want toomanage your costs and limit hello amount of data collected for a solution by limiting it tooa particular set of agents.</span></span>  <span data-ttu-id="333bb-107">이 문서에서는 설명 방법을 toouse **솔루션을 대상으로** tooapply 범위를 허용 하는 OMS 기능 되 tooyour 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-107">This article describes how toouse **Solution Targeting** which is an OMS feature that allows you tooapply a scope tooyour solutions.</span></span>

## <a name="how-tootarget-a-solution"></a><span data-ttu-id="333bb-108">어떻게 tootarget 솔루션</span><span class="sxs-lookup"><span data-stu-id="333bb-108">How tootarget a solution</span></span>
<span data-ttu-id="333bb-109">있는 경우 3 단계 tootargeting 솔루션 hello 다음 섹션에에서 설명 된 대로</span><span class="sxs-lookup"><span data-stu-id="333bb-109">There are three steps tootargeting a solution as described in hello following sections.</span></span>  <span data-ttu-id="333bb-110">Note 다른 단계에 대 한 hello OMS 포털 및 hello Azure 포털 둘 다 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-110">Note that you will need both hello OMS portal and hello Azure portal for different steps.</span></span>


### <a name="1-create-a-computer-group"></a><span data-ttu-id="333bb-111">1. 컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="333bb-111">1. Create a computer group</span></span>
<span data-ttu-id="333bb-112">Hello 컴퓨터를 만들어 범위에서 tooinclude 한다는 것을 지정 된 [컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md) 로그 분석에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-112">You specify hello computers that you want tooinclude in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span></span>  <span data-ttu-id="333bb-113">hello 컴퓨터 그룹을 로그 검색에 따라 또는 Active Directory 또는 WSUS 그룹 등의 다른 원본에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-113">hello computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span></span> <span data-ttu-id="333bb-114">으로 [아래에 설명 된](#solutions-and-agents-that-cant-be-targeted)직접 컴퓨터 연결 tooLog 분석 hello 범위에 포함 될 것만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-114">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected tooLog Analytics will be included in hello scope.</span></span>

<span data-ttu-id="333bb-115">Hello 컴퓨터 그룹 작업 영역에서 만든를 만든 후 다음 수에 포함 하 적용된 tooone 또는 많은 해결 될 수 있는 범위 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-115">Once you have hello computer group created in your workspace, then you'll include it in a scope configuration that can be applied tooone or more solutions.</span></span>
 
 
 ### <a name="2-create-a-scope-configuration"></a><span data-ttu-id="333bb-116">2. 범위 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="333bb-116">2. Create a scope configuration</span></span>
 <span data-ttu-id="333bb-117">A **범위 구성** 하나 이상의 컴퓨터 그룹을 포함 하며 적용된 tooone 또는 많은 해결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-117">A **Scope Configuration** includes one or more computer groups and can be applied tooone or more solutions.</span></span> 
 
 <span data-ttu-id="333bb-118">다음 프로세스를 수행 하는 hello를 사용 하 여 범위 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-118">Create a scope configuration using hello following process.</span></span>  

 1. <span data-ttu-id="333bb-119">Hello Azure 포털에서 탐색 너무**로그 분석** 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-119">In hello Azure portal, navigate too**Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="333bb-120">Hello 작업 영역에 대 한 hello 속성에서 **작업 영역 데이터 원본** 선택 **범위 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-120">In hello properties for hello workspace under **Workspace Data Sources** select **Scope Configurations**.</span></span>
 3. <span data-ttu-id="333bb-121">클릭 **추가** toocreate 새 범위 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-121">Click **Add** toocreate a new scope configuration.</span></span>
 4. <span data-ttu-id="333bb-122">입력 **이름** hello 범위 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-122">Type a **Name** for hello scope configuration.</span></span>
 5. <span data-ttu-id="333bb-123">**컴퓨터 그룹 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-123">Click **Select Computer Groups**.</span></span>
 6. <span data-ttu-id="333bb-124">만든 hello 컴퓨터 그룹 및 필요에 따라 다른 그룹 tooadd toohello 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-124">Select hello computer group that you created and optionally any other groups tooadd toohello configuration.</span></span>  <span data-ttu-id="333bb-125">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-125">Click **Select**.</span></span>  
 6. <span data-ttu-id="333bb-126">클릭 **확인** toocreate hello 범위 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-126">Click **OK** toocreate hello scope configuration.</span></span> 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a><span data-ttu-id="333bb-127">3. Hello 범위 구성 tooa 솔루션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-127">3. Apply hello scope configuration tooa solution.</span></span>
<span data-ttu-id="333bb-128">있으면 범위 구성을 tooone 또는 많은 해결 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-128">Once you have a scope configuration, then you can apply it tooone or more solutions.</span></span>  <span data-ttu-id="333bb-129">단일 범위 구성을 여러 솔루션에서 사용할 수 있지만, 각 솔루션은 범위 구성을 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-129">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span></span>

<span data-ttu-id="333bb-130">다음 프로세스를 수행 하는 hello를 사용 하 여 범위 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-130">Apply a scope configuration using hello following process.</span></span>  

 1. <span data-ttu-id="333bb-131">Hello Azure 포털에서 탐색 너무**로그 분석** 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-131">In hello Azure portal, navigate too**Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="333bb-132">Hello 작업 영역에 대 한 hello 속성에서 선택 **솔루션**합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-132">In hello properties for hello workspace select **Solutions**.</span></span>
 3. <span data-ttu-id="333bb-133">클릭 tooscope hello 솔루션에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-133">Click on hello solution you want tooscope.</span></span>
 4. <span data-ttu-id="333bb-134">Hello 솔루션에 대 한 hello 속성의 **작업 영역 데이터 원본** 선택 **솔루션을 대상으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-134">In hello properties for hello solution under **Workspace Data Sources** select **Solution Targeting**.</span></span>  <span data-ttu-id="333bb-135">Hello 옵션을 사용할 수 없는 경우 다음 [이 솔루션을 대상으로 지정할 수](#solutions-and-agents-that-cant-be-targeted)합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-135">If hello option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span></span>
 5. <span data-ttu-id="333bb-136">**범위 구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-136">Click **Add scope configuration**.</span></span>  <span data-ttu-id="333bb-137">적용 된 구성을 toothis 솔루션이 이미 있는 경우 다음이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-137">If you already have a configuration applied toothis solution then this option will be unavailable.</span></span>  <span data-ttu-id="333bb-138">추가 하기 전에 다른 hello 기존 구성을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-138">You must remove hello existing configuration before adding another one.</span></span>
 6. <span data-ttu-id="333bb-139">만든 hello 범위 구성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-139">Click on hello scope configuration that you created.</span></span>
 7. <span data-ttu-id="333bb-140">조사식 hello **상태** 표시 hello 구성 tooensure의 **Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-140">Watch hello **Status** of hello configuration tooensure that it shows **Succeeded**.</span></span>  <span data-ttu-id="333bb-141">Hello 구성 및 선택의 hello 타원 toohello 오른쪽 클릭 hello 상태 오류가 나타나면 **편집 범위 구성** toomake 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-141">If hello status indicates an error, then click hello ellipse toohello right of hello configuration and select **Edit scope configuration** toomake changes.</span></span>

## <a name="solutions-and-agents-that-cant-be-targeted"></a><span data-ttu-id="333bb-142">대상으로 지정할 수 없는 솔루션 및 에이전트</span><span class="sxs-lookup"><span data-stu-id="333bb-142">Solutions and agents that can't be targeted</span></span>
<span data-ttu-id="333bb-143">다음은 에이전트와 솔루션을 대상으로 함께 사용할 수 없는 솔루션에 대 한 hello 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-143">Following are hello criteria for agents and solutions that can't be used with solution targeting.</span></span>

- <span data-ttu-id="333bb-144">솔루션을 대상으로 tooagents 배포 toosolutions만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-144">Solution targeting only applies toosolutions that deploy tooagents.</span></span>
- <span data-ttu-id="333bb-145">솔루션을 대상으로 Microsoft에서 제공 하는 toosolutions만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-145">Solution targeting only applies toosolutions provided by Microsoft.</span></span>  <span data-ttu-id="333bb-146">Toosolutions는 적용 되지 않습니다 [직접 만들거나 파트너 만든](operations-management-suite-solutions-creating.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-146">It does not apply toosolutions [created by yourself or partners](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="333bb-147">TooLog 분석에 직접 연결 하는 에이전트만 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-147">You can only filter out agents that connect directly tooLog Analytics.</span></span>  <span data-ttu-id="333bb-148">솔루션에서 자동으로 범위 구성에 포함 하는 지 여부는 연결 된 Operations Manager 관리 그룹의 일부인 tooany 에이전트를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-148">Solutions will automatically deploy tooany agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span></span>

### <a name="exceptions"></a><span data-ttu-id="333bb-149">예외</span><span class="sxs-lookup"><span data-stu-id="333bb-149">Exceptions</span></span>
<span data-ttu-id="333bb-150">Hello로 솔루션을 대상으로 사용할 수 없습니다 명시 된 조건을 hello에 맞을 경우에 솔루션을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-150">Solution targeting cannot be used with hello following solutions even though they fit hello stated criteria.</span></span>

- <span data-ttu-id="333bb-151">에이전트 상태 평가</span><span class="sxs-lookup"><span data-stu-id="333bb-151">Agent Health Assessment</span></span>

## <a name="next-steps"></a><span data-ttu-id="333bb-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="333bb-152">Next steps</span></span>
- <span data-ttu-id="333bb-153">사용자 환경에서 사용할 수 있는 tooinstall 않는 hello 솔루션을 비롯 한 관리 솔루션에 대 한 자세한 [추가 Azure 로그 분석 관리 솔루션 tooyour 작업 영역](../log-analytics/log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="333bb-153">Learn more about management solutions including hello solutions that are available tooinstall in your environment at [Add Azure Log Analytics management solutions tooyour workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
- <span data-ttu-id="333bb-154">[Log Analytics 로그 검색의 컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md)에서 컴퓨터 그룹 생성에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="333bb-154">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span></span>
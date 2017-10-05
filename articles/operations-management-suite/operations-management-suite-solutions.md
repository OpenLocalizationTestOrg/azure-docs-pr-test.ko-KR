---
title: "OMS(Operations Management Suite)의 솔루션 | Microsoft Docs"
description: "솔루션은 고객이 OMS 작업 영역에 추가할 수 있는 패키지 관리 시나리오를 제공하여 OMS(Operations Management Suite)의 기능을 확장합니다.  이 문서에서는 고객 및 파트너가 사용자 지정 솔루션을 만드는 방법에 대한 세부 정보를 제공합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2443dd73fdf441721bd6f6f340da515d9f5a22a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a><span data-ttu-id="ac577-104">OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="ac577-104">Working with management solutions in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="ac577-105">현재 Preview로 제공되는 OMS의 관리 솔루션에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-105">This is preliminary documentation for management solutions in OMS which are currently in preview.</span></span>    
> 
> 

<span data-ttu-id="ac577-106">관리 솔루션은 고객이 환경에 추가할 수 있는 패키지 관리 시나리오를 제공하여 OMS(Operations Management Suite)의 기능을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-106">Management solutions extend the functionality of Operations Management Suite (OMS) by providing packaged management scenarios that customers can add to their environment.</span></span>  <span data-ttu-id="ac577-107">[Microsoft에서 제공한 솔루션](../log-analytics/log-analytics-add-solutions.md) 외에도 파트너 및 고객은 자신의 환경에서 사용하거나 커뮤니티를 통해 고객이 이용할 수 있는 관리 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-107">In addition to [solutions provided by Microsoft](../log-analytics/log-analytics-add-solutions.md), partners and customers can create management solutions to be used in their own environment or made available to customers through the community.</span></span>

## <a name="finding-and-installing-management-solutions"></a><span data-ttu-id="ac577-108">관리 솔루션 찾기 및 설치</span><span class="sxs-lookup"><span data-stu-id="ac577-108">Finding and installing management solutions</span></span>
<span data-ttu-id="ac577-109">다음 섹션에 설명된 대로 관리 솔루션을 찾아 설치하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-109">There are multiple methods for locating and installing management solutions as described in the following sections.</span></span>

### <a name="azure-marketplace"></a><span data-ttu-id="ac577-110">Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="ac577-110">Azure Marketplace</span></span>
<span data-ttu-id="ac577-111">Microsoft 및 신뢰할 수 있는 파트너에서 제공한 관리 솔루션은 Azure Portal의 Azure Marketplace로부터 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-111">Management solutions provided by Microsoft and trusted partners may be installed from the Azure Marketplace in the Azure portal.</span></span>

1. <span data-ttu-id="ac577-112">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-112">Log in to the Azure portal.</span></span>
2. <span data-ttu-id="ac577-113">왼쪽 창에서 **더 많은 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-113">In the left pane, select **More services**.</span></span>
3. <span data-ttu-id="ac577-114">**솔루션**까지 아래로 스크롤하거나 **필터** 대화 상자에 *솔루션*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-114">Either scroll down to **Solutions** or type *solutions* into the **Filter** dialog.</span></span>
4. <span data-ttu-id="ac577-115">**+추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-115">Click the **+ Add** button.</span></span>
5. <span data-ttu-id="ac577-116">찾아보거나 **필터** 단추를 클릭하거나 **모두 검색** 상자에 입력하여 관심 있는 솔루션을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-116">Search for solutions that you're interested in either by browsing, clicking the **Filter** button, or typing in the **Search Everthing** box.</span></span>
6. <span data-ttu-id="ac577-117">해당 세부 정보를 보려면 마켓플레이스 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-117">Click a marketplace item to view its detailed information.</span></span>
7. <span data-ttu-id="ac577-118">**만들기**를 클릭하여 **솔루션 추가** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-118">Click **Create** to open the **Add Solution** pane.</span></span>
8. <span data-ttu-id="ac577-119">솔루션의 모든 매개 변수에 대한 값 외에도 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account)과 같은 필수 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-119">You will be prompted to required information such as the [OMS workspace and Automation account](#oms-workspace-and-automation-account) in addition to values for any parameters in the solution.</span></span>
9. <span data-ttu-id="ac577-120">**만들기**를 클릭하여 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-120">Click **Create** to install the solution.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="ac577-121">OMS 포털</span><span class="sxs-lookup"><span data-stu-id="ac577-121">OMS Portal</span></span>
<span data-ttu-id="ac577-122">OMS 포털의 솔루션 갤러리로부터 Microsoft에서 제공하는 관리 솔루션을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-122">Management solutions provided by Microsoft may be installed from the Solutions Gallery in the OMS portal.</span></span>

1. <span data-ttu-id="ac577-123">OMS 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-123">Log in to the OMS portal.</span></span>
2. <span data-ttu-id="ac577-124">**솔루션 갤러리** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-124">Click the **Solutions Gallery** tile.</span></span>
3. <span data-ttu-id="ac577-125">OMS 솔루션 갤러리 페이지에서 사용 가능한 각 솔루션에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-125">On the OMS Solutions Gallery page, learn about each available solution.</span></span> <span data-ttu-id="ac577-126">OMS에 추가할 솔루션의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-126">Click the name of the solution that you want to add to OMS.</span></span>
4. <span data-ttu-id="ac577-127">선택한 솔루션에 대한 페이지에서 솔루션에 대한 자세한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-127">On the page for the solution that you chose, detailed information about the solution is displayed.</span></span> <span data-ttu-id="ac577-128">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-128">Click **Add**.</span></span>
5. <span data-ttu-id="ac577-129">추가한 솔루션의 새 타일이 OMS의 개요 페이지에 표시되며 OMS 서비스가 데이터를 처리한 후 새 타일을 사용하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-129">A new tile for the solution that you added appears on the Overview page in OMS and you can start using it after the OMS service processes your data.</span></span>

### <a name="azure-quickstart-templates"></a><span data-ttu-id="ac577-130">Azure 빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="ac577-130">Azure Quickstart Templates</span></span>
<span data-ttu-id="ac577-131">커뮤니티 구성원은 관리 솔루션을 Azure 빠른 시작 템플릿에 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-131">Members of the community can submit management solutions to Azure Quickstart Templates.</span></span>  <span data-ttu-id="ac577-132">이 템플릿을 다운로드하여 나중에 설치하거나 템플릿을 검사하여 [사용자 고유의 솔루션을 만드는](#creating-a-solution) 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-132">You can either download these templates for later installation or inspect them to learn how to [create your own solutions](#creating-a-solution).</span></span>

1. <span data-ttu-id="ac577-133">[OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account)에 설명된 프로세스에 따라 작업 영역 및 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-133">Follow the process described in [OMS workspace and Automation account](#oms-workspace-and-automation-account) to link a workspace and account.</span></span>
2. <span data-ttu-id="ac577-134">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-134">Go to [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>  
3. <span data-ttu-id="ac577-135">관심 있는 솔루션을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-135">Search for a solution that you're interested in.</span></span>
4. <span data-ttu-id="ac577-136">해당 정보를 보려면 결과에서 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-136">Select the solution from the results to view its details.</span></span>
5. <span data-ttu-id="ac577-137">**Azure에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-137">Click the **Deploy to Azure** button.</span></span>
6. <span data-ttu-id="ac577-138">솔루션의 모든 매개 변수에 대한 값 외에도 리소스 그룹 및 위치와 같은 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-138">You will be prompted to provide information such as the resource group and location in addition to values for any parameters in the solution.</span></span>
7. <span data-ttu-id="ac577-139">**구매**를 클릭하여 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-139">Click **Purchase** to install the solution.</span></span>

### <a name="deploy-azure-resource-manager-template"></a><span data-ttu-id="ac577-140">Azure Resource Manager 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="ac577-140">Deploy Azure Resource Manager template</span></span>
<span data-ttu-id="ac577-141">커뮤니티에서 가져오거나 사용자가 [직접 만든](#creating-a-solution) 솔루션은 Resource Manager 템플릿으로 구현되며, [템플릿 배포](../azure-resource-manager/resource-group-template-deploy-portal.md)를 위한 표준 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-141">Solutions that you get from the community or that you [create yourself](#creating-a-solution) are implemented as a Resource Manager template, and you can use any of the standard methods for [deploying a template](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>  <span data-ttu-id="ac577-142">솔루션을 설치하기 전에 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account)을 만들어 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-142">Note that before installing the solution, you must create and link the [OMS workspace and Automation account](#oms-workspace-and-automation-account).</span></span>

## <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="ac577-143">OMS 작업 영역 및 자동화 계정</span><span class="sxs-lookup"><span data-stu-id="ac577-143">OMS workspace and Automation account</span></span>
<span data-ttu-id="ac577-144">대부분의 관리 솔루션은 뷰를 포함하는 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md)과 Runbook 및 관련 리소스를 포함하는 [자동화 계정](../automation/automation-security-overview.md#automation-account-overview)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-144">Most management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span> <span data-ttu-id="ac577-145">작업 영역 및 계정은 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-145">The workspace and account must meet the following requirements.</span></span>

* <span data-ttu-id="ac577-146">솔루션은 하나의 OMS 작업 영역과 하나의 자동화 계정만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-146">A solution can only use one OMS workspace and one Automation account.</span></span>  
* <span data-ttu-id="ac577-147">솔루션이 사용하는 OMS 작업 영역과 자동화 계정은 서로 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-147">The OMS workspace and Automation account used by a solution must be linked to one another.</span></span> <span data-ttu-id="ac577-148">OMS 작업 영역은 하나의 자동화 계정에만 연결되고, 자동화 계정은 하나의 OMS 작업 영역에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-148">An OMS workspace may only be linked to one Automation account, and an Automation account may only be linked to one OMS workspace.</span></span>
* <span data-ttu-id="ac577-149">연결하려면 OMS 작업 영역 및 자동화 계정은 동일한 리소스 그룹 및 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-149">To be linked, the OMS workspace and Automation account must be in the same resource group and region.</span></span>  <span data-ttu-id="ac577-150">미국 동부 지역에 있는 OMS 작업 영역과 미국 동부 2에 있는 자동화 계정의 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-150">The exception is an OMS workspace in East US region and and Automation account in East US 2.</span></span>

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="ac577-151">OMS 작업 영역 및 자동화 계정 간의 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="ac577-151">Creating a link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="ac577-152">OMS 작업 영역 및 자동화 계정을 지정하는 방법은 솔루션의 설치 방법에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-152">How you specify the OMS workspace and Automation account depends on the installation method for your solution.</span></span>

* <span data-ttu-id="ac577-153">OMS 포털을 통해 Microsoft 솔루션을 설치하는 경우 현재 OMS 작업 영역에 설치되며 자동화 계정은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-153">When you install a Microsoft solution through the OMS portal, it is installed in the current OMS workspace and no Automation account is required.</span></span>
* <span data-ttu-id="ac577-154">Azure Marketplace를 통해 솔루션을 설치하는 경우 OMS 작업 영역 및 자동화 계정에 대한 메시지가 표시되고 이들 간에 링크가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-154">When you install a solution through the Azure Marketplace, you are prompted for an OMS workspace and Automation account, and the link between them is created for you.</span></span>  
* <span data-ttu-id="ac577-155">Azure Marketplace의 외부 솔루션의 경우 솔루션을 설치하기 전에 OMS 작업 영역 및 자동화 계정을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-155">For solutions outside of the Azure Marketplace, you must link the OMS workspace and Automation account before installing the solution.</span></span>  <span data-ttu-id="ac577-156">Azure Marketplace에서 솔루션을 선택하고 OMS 작업 영역 및 자동화 계정을 선택하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-156">You can do this by selecting any solution in the Azure Marketplace and selecting the OMS workspace and Automation account.</span></span>  <span data-ttu-id="ac577-157">OMS 작업 영역 및 자동화 계정을 선택하는 즉시 링크가 만들어지기 때문에 솔루션을 직접 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-157">You don't have to actually install the solution because the link will be created as soon as the OMS workspace and Automation account are selected.</span></span>  <span data-ttu-id="ac577-158">링크가 만들어지면 솔루션의 해당 OMS 작업 영역 및 자동화 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-158">Once the link is created, then you can use that OMS workspace and Automation account for any solution.</span></span> 

### <a name="verifying-the-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="ac577-159">OMS 작업 영역 및 자동화 계정 간의 링크 확인하기</span><span class="sxs-lookup"><span data-stu-id="ac577-159">Verifying the link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="ac577-160">다음 절차를 통해 OMS 작업 영역 및 자동화 계정 간의 링크를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-160">You can verify the link between an OMS workspace and an Automation account using the following procedure.</span></span>

1. <span data-ttu-id="ac577-161">Azure Portal에서 자동화 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-161">Select the Automation account in the Azure portal.</span></span>
2. <span data-ttu-id="ac577-162">**설정** 창의 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-162">Scroll to the bottom of the **Settings** pane.</span></span>
3. <span data-ttu-id="ac577-163">**설정** 창에 **OMS 리소스**라는 섹션이 있는 경우 이 계정은 OMS 작업 영역에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-163">If there is a section called **OMS Resources** in the **Settings** pane, then this account is attached to an OMS workspace.</span></span>
4. <span data-ttu-id="ac577-164">**작업 영역**을 선택하여 이 자동화 계정에 연결된 OMS 작업 영역의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-164">Select **Workspace** to view the details of the OMS workspace linked to this Automation account.</span></span>

## <a name="listing-management-solutions"></a><span data-ttu-id="ac577-165">목록 관리 솔루션</span><span class="sxs-lookup"><span data-stu-id="ac577-165">Listing management solutions</span></span>
<span data-ttu-id="ac577-166">다음 절차를 통해 Azure 구독에 연결된 작업 영역에 있는 관리 솔루션을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-166">Use the following procedure to to view the management solutions in the workspaces linked to your Azure subscription.</span></span>

1. <span data-ttu-id="ac577-167">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-167">Log in to the Azure portal.</span></span>
2. <span data-ttu-id="ac577-168">왼쪽 창에서 **더 많은 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-168">In the left pane, select **More services**.</span></span>
3. <span data-ttu-id="ac577-169">**솔루션**까지 아래로 스크롤하거나 **필터** 대화 상자에 *솔루션*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-169">Either scroll down to **Solutions** or type *solutions* into the **Filter** dialog.</span></span>
4. <span data-ttu-id="ac577-170">모든 작업 영역에 설치된 솔루션이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-170">Solutions installed in all your workspaces will be listed.</span></span>

<span data-ttu-id="ac577-171">OMS 포털을 사용하면 현재 작업 영역에 설치된 Microsoft 솔루션만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-171">Note that you can view only the Microsoft solutions installed in the current workspace using the OMS portal.</span></span>

## <a name="removing-a-management-solution"></a><span data-ttu-id="ac577-172">관리 솔루션 제거</span><span class="sxs-lookup"><span data-stu-id="ac577-172">Removing a management solution</span></span>
<span data-ttu-id="ac577-173">관리 솔루션을 제거하면 솔루션의 모든 리소스도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-173">When a management solution is removed, all resources in the solution are also removed.</span></span>  

1. <span data-ttu-id="ac577-174">[솔루션 나열](#listing-solutions)의 절차를 통해 Azure Portal에서 솔루션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-174">Locate the solution in the Azure portal using the procedure in [Listing solutions](#listing-solutions).</span></span>
2. <span data-ttu-id="ac577-175">제거하려는 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-175">Select the solution you want to remove.</span></span>
3. <span data-ttu-id="ac577-176">**삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-176">Click the **Delete** button.</span></span>

## <a name="creating-a-management-solution"></a><span data-ttu-id="ac577-177">관리 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="ac577-177">Creating a management solution</span></span>
<span data-ttu-id="ac577-178">관리 솔루션 만들기에 대한 전체 지침은 [OMS(Operations Management Suite)](operations-management-suite-solutions-creating.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-178">Complete guidance on creating management solutions are available at [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ac577-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac577-179">Next steps</span></span>
* <span data-ttu-id="ac577-180">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-180">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
* <span data-ttu-id="ac577-181">자신만의 [관리 솔루션](operations-management-suite-solutions-creating.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac577-181">Create your own [management solutions](operations-management-suite-solutions-creating.md).</span></span>


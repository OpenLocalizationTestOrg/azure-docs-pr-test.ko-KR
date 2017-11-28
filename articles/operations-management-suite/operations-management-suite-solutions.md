---
title: "Operations Management Suite (OMS)에서 aaaSolutions | Microsoft Docs"
description: "패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 솔루션을 고객 tootheir OMS 작업 영역을 추가할 수 있습니다.  이 문서에서는 고객 및 파트너가 사용자 지정 솔루션을 만드는 방법에 대한 세부 정보를 제공합니다."
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
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a><span data-ttu-id="31c83-104">OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="31c83-104">Working with management solutions in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="31c83-105">현재 Preview로 제공되는 OMS의 관리 솔루션에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-105">This is preliminary documentation for management solutions in OMS which are currently in preview.</span></span>    
> 
> 

<span data-ttu-id="31c83-106">패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 관리 솔루션을 고객 tootheir 환경에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-106">Management solutions extend hello functionality of Operations Management Suite (OMS) by providing packaged management scenarios that customers can add tootheir environment.</span></span>  <span data-ttu-id="31c83-107">또한 너무[Microsoft에서 제공 하는 솔루션](../log-analytics/log-analytics-add-solutions.md), 파트너 및 고객 관리 솔루션 toobe 자신의 환경에서 사용 되거나 hello 커뮤니티를 통해 사용할 수 있는 toocustomers 있게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-107">In addition too[solutions provided by Microsoft](../log-analytics/log-analytics-add-solutions.md), partners and customers can create management solutions toobe used in their own environment or made available toocustomers through hello community.</span></span>

## <a name="finding-and-installing-management-solutions"></a><span data-ttu-id="31c83-108">관리 솔루션 찾기 및 설치</span><span class="sxs-lookup"><span data-stu-id="31c83-108">Finding and installing management solutions</span></span>
<span data-ttu-id="31c83-109">찾기 및 hello 다음 섹션에에서 설명 된 대로 관리 솔루션을 설치 하기 위한 여러 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-109">There are multiple methods for locating and installing management solutions as described in hello following sections.</span></span>

### <a name="azure-marketplace"></a><span data-ttu-id="31c83-110">Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="31c83-110">Azure Marketplace</span></span>
<span data-ttu-id="31c83-111">Microsoft에서 관리 솔루션을 제공 하 고 신뢰할 수 있는 파트너 hello Azure 포털에서에서 Azure 마켓플레이스 hello에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-111">Management solutions provided by Microsoft and trusted partners may be installed from hello Azure Marketplace in hello Azure portal.</span></span>

1. <span data-ttu-id="31c83-112">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-112">Log in toohello Azure portal.</span></span>
2. <span data-ttu-id="31c83-113">Hello 왼쪽된 창에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-113">In hello left pane, select **More services**.</span></span>
3. <span data-ttu-id="31c83-114">너무 아래로 스크롤하여 하나**솔루션** 또는 형식 *솔루션* hello에 **필터** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="31c83-114">Either scroll down too**Solutions** or type *solutions* into hello **Filter** dialog.</span></span>
4. <span data-ttu-id="31c83-115">Hello 클릭 **+ 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-115">Click hello **+ Add** button.</span></span>
5. <span data-ttu-id="31c83-116">를 찾아 중 하나에 관심이 있는 솔루션에 대 한 검색 hello를 클릭 하면 **필터** 단추 또는 hello에 입력 **검색 칸씩** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-116">Search for solutions that you're interested in either by browsing, clicking hello **Filter** button, or typing in hello **Search Everthing** box.</span></span>
6. <span data-ttu-id="31c83-117">마켓플레이스 항목 tooview 해당 세부 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-117">Click a marketplace item tooview its detailed information.</span></span>
7. <span data-ttu-id="31c83-118">클릭 **만들기** tooopen hello **솔루션 추가** 창.</span><span class="sxs-lookup"><span data-stu-id="31c83-118">Click **Create** tooopen hello **Add Solution** pane.</span></span>
8. <span data-ttu-id="31c83-119">Hello 같은 증명된 toorequired 정보 됩니다 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account) 또한 매개 변수에 대해 toovalues hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-119">You will be prompted toorequired information such as hello [OMS workspace and Automation account](#oms-workspace-and-automation-account) in addition toovalues for any parameters in hello solution.</span></span>
9. <span data-ttu-id="31c83-120">클릭 **만들기** tooinstall hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-120">Click **Create** tooinstall hello solution.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="31c83-121">OMS 포털</span><span class="sxs-lookup"><span data-stu-id="31c83-121">OMS Portal</span></span>
<span data-ttu-id="31c83-122">Microsoft에서 제공 하는 관리 솔루션에서 솔루션 갤러리 hello hello OMS 포털에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-122">Management solutions provided by Microsoft may be installed from hello Solutions Gallery in hello OMS portal.</span></span>

1. <span data-ttu-id="31c83-123">OMS 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-123">Log in toohello OMS portal.</span></span>
2. <span data-ttu-id="31c83-124">Hello 클릭 **솔루션 갤러리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-124">Click hello **Solutions Gallery** tile.</span></span>
3. <span data-ttu-id="31c83-125">Hello OMS 솔루션 갤러리 페이지에서 사용 가능한 각 솔루션에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-125">On hello OMS Solutions Gallery page, learn about each available solution.</span></span> <span data-ttu-id="31c83-126">Tooadd tooOMS hello 솔루션의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-126">Click hello name of hello solution that you want tooadd tooOMS.</span></span>
4. <span data-ttu-id="31c83-127">선택한 hello 솔루션에 대 한 hello 페이지 hello 솔루션에 대 한 자세한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-127">On hello page for hello solution that you chose, detailed information about hello solution is displayed.</span></span> <span data-ttu-id="31c83-128">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-128">Click **Add**.</span></span>
5. <span data-ttu-id="31c83-129">Hello OMS 서비스가 데이터를 처리 한 후 사용을 시작 하 고 hello OMS의 개요 페이지에 표시 추가 hello 솔루션에 대 한 새 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-129">A new tile for hello solution that you added appears on hello Overview page in OMS and you can start using it after hello OMS service processes your data.</span></span>

### <a name="azure-quickstart-templates"></a><span data-ttu-id="31c83-130">Azure 빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="31c83-130">Azure Quickstart Templates</span></span>
<span data-ttu-id="31c83-131">Hello 커뮤니티의 회원과 관리 솔루션 tooAzure 퀵 스타트 서식 파일을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-131">Members of hello community can submit management solutions tooAzure Quickstart Templates.</span></span>  <span data-ttu-id="31c83-132">이후 설치에 대 한 이러한 서식 파일을 다운로드 하거나 검사 toolearn 어떻게 너무[사용자 고유의 솔루션을 만들](#creating-a-solution)합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-132">You can either download these templates for later installation or inspect them toolearn how too[create your own solutions](#creating-a-solution).</span></span>

1. <span data-ttu-id="31c83-133">에 설명 된 hello 프로세스에 따라 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account) toolink 작업 영역 및 계정.</span><span class="sxs-lookup"><span data-stu-id="31c83-133">Follow hello process described in [OMS workspace and Automation account](#oms-workspace-and-automation-account) toolink a workspace and account.</span></span>
2. <span data-ttu-id="31c83-134">너무 이동[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-134">Go too[Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>  
3. <span data-ttu-id="31c83-135">관심 있는 솔루션을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-135">Search for a solution that you're interested in.</span></span>
4. <span data-ttu-id="31c83-136">세부 정보에서 hello 결과 tooview hello 솔루션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-136">Select hello solution from hello results tooview its details.</span></span>
5. <span data-ttu-id="31c83-137">Hello 클릭 **tooAzure 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-137">Click hello **Deploy tooAzure** button.</span></span>
6. <span data-ttu-id="31c83-138">Hello 리소스 그룹 및 hello 솔루션의 모든 매개 변수에 대 한 추가 toovalues의 위치와 같은 증명된 tooprovide 정보 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-138">You will be prompted tooprovide information such as hello resource group and location in addition toovalues for any parameters in hello solution.</span></span>
7. <span data-ttu-id="31c83-139">클릭 **구매** tooinstall hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-139">Click **Purchase** tooinstall hello solution.</span></span>

### <a name="deploy-azure-resource-manager-template"></a><span data-ttu-id="31c83-140">Azure Resource Manager 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="31c83-140">Deploy Azure Resource Manager template</span></span>
<span data-ttu-id="31c83-141">Hello 커뮤니티 하거나에서 얻을 수 있는 솔루션 [사용자가 직접 만든](#creating-a-solution) 리소스 관리자 템플릿으로 구현 hello에 대 한 표준 방법 중 하나를 사용할 수 있습니다 [서식 파일 배포](../azure-resource-manager/resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-141">Solutions that you get from hello community or that you [create yourself](#creating-a-solution) are implemented as a Resource Manager template, and you can use any of hello standard methods for [deploying a template](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>  <span data-ttu-id="31c83-142">참고는 hello 솔루션을 설치 하기 전에 해야을 만든 다음 연결 hello [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-142">Note that before installing hello solution, you must create and link hello [OMS workspace and Automation account](#oms-workspace-and-automation-account).</span></span>

## <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="31c83-143">OMS 작업 영역 및 Automation 계정</span><span class="sxs-lookup"><span data-stu-id="31c83-143">OMS workspace and Automation account</span></span>
<span data-ttu-id="31c83-144">대부분의 관리 솔루션에 필요한는 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md) toocontain 뷰 및 [자동화 계정](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook 및 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-144">Most management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span> <span data-ttu-id="31c83-145">작업 영역을 hello 및 계정은 hello 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-145">hello workspace and account must meet hello following requirements.</span></span>

* <span data-ttu-id="31c83-146">솔루션은 하나의 OMS 작업 영역과 하나의 자동화 계정만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-146">A solution can only use one OMS workspace and one Automation account.</span></span>  
* <span data-ttu-id="31c83-147">hello OMS 작업 영역 및 솔루션에서 사용 되는 자동화 계정 해야 tooone 연결 된 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-147">hello OMS workspace and Automation account used by a solution must be linked tooone another.</span></span> <span data-ttu-id="31c83-148">OMS 작업 영역 연결된 tooone 자동화 계정에만 사용할 수 있습니다 및 자동화 계정을 연결 된 tooone OMS 작업 영역 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-148">An OMS workspace may only be linked tooone Automation account, and an Automation account may only be linked tooone OMS workspace.</span></span>
* <span data-ttu-id="31c83-149">자동화 계정에 있어야 합니다. 리소스 그룹 및 지역이 동일한 hello 되었으며 toobe hello OMS 작업 영역 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-149">toobe linked, hello OMS workspace and Automation account must be in hello same resource group and region.</span></span>  <span data-ttu-id="31c83-150">hello 예외는 미국 동부 지역에 OMS 작업 영역 및 및 미국 동부 2의에서 자동화 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-150">hello exception is an OMS workspace in East US region and and Automation account in East US 2.</span></span>

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="31c83-151">OMS 작업 영역 및 자동화 계정 간의 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="31c83-151">Creating a link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="31c83-152">어떻게 hello OMS 작업 영역을 지정 하 고 자동화 계정 솔루션에 대 한 hello 설치 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-152">How you specify hello OMS workspace and Automation account depends on hello installation method for your solution.</span></span>

* <span data-ttu-id="31c83-153">Hello OMS 포털을 통해 Microsoft 솔루션을 설치 하면 hello 현재 OMS 작업 영역에 설치 되며 자동화 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-153">When you install a Microsoft solution through hello OMS portal, it is installed in hello current OMS workspace and no Automation account is required.</span></span>
* <span data-ttu-id="31c83-154">Hello Azure 마켓플레이스를 통해 솔루션을 설치 하면 OMS 작업 영역 및 자동화 계정에 대 한 메시지가 표시 되 및 서로 hello 링크 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-154">When you install a solution through hello Azure Marketplace, you are prompted for an OMS workspace and Automation account, and hello link between them is created for you.</span></span>  
* <span data-ttu-id="31c83-155">Hello Azure 마켓플레이스에서 외부에서 솔루션을 OMS 작업 영역 hello 및 자동화 계정 hello 솔루션을 설치 하기 전에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-155">For solutions outside of hello Azure Marketplace, you must link hello OMS workspace and Automation account before installing hello solution.</span></span>  <span data-ttu-id="31c83-156">Hello Azure Marketplace에서에서 모든 솔루션을 선택 하 고 hello OMS 작업 영역 및 자동화 계정을 선택 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-156">You can do this by selecting any solution in hello Azure Marketplace and selecting hello OMS workspace and Automation account.</span></span>  <span data-ttu-id="31c83-157">Tooactually hello OMS 작업 영역 및 자동화 계정을 선택 하는 즉시 hello 링크를 만들 수는 없으므로 hello 솔루션을 설치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-157">You don't have tooactually install hello solution because hello link will be created as soon as hello OMS workspace and Automation account are selected.</span></span>  <span data-ttu-id="31c83-158">Hello 링크를 만든 후 사용할 수 있습니다 OMS 작업 영역 및 자동화 계정을 하는 모든 솔루션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-158">Once hello link is created, then you can use that OMS workspace and Automation account for any solution.</span></span> 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="31c83-159">OMS 작업 영역 및 자동화 계정 간의 hello 링크를 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="31c83-159">Verifying hello link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="31c83-160">OMS 작업 영역 및 절차를 수행 하는 hello를 사용 하 여 자동화 계정 간의 hello 링크를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-160">You can verify hello link between an OMS workspace and an Automation account using hello following procedure.</span></span>

1. <span data-ttu-id="31c83-161">Hello Azure 포털에서에서 hello 자동화 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-161">Select hello Automation account in hello Azure portal.</span></span>
2. <span data-ttu-id="31c83-162">Hello toohello 맨 아래로 스크롤 **설정을** 창.</span><span class="sxs-lookup"><span data-stu-id="31c83-162">Scroll toohello bottom of hello **Settings** pane.</span></span>
3. <span data-ttu-id="31c83-163">섹션이 없는 경우 **OMS 리소스** hello에 **설정을** 창에서이 계정을 연결 된 tooan OMS 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-163">If there is a section called **OMS Resources** in hello **Settings** pane, then this account is attached tooan OMS workspace.</span></span>
4. <span data-ttu-id="31c83-164">선택 **작업 영역** hello OMS 작업 영역의 tooview hello 세부 정보 toothis 자동화 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-164">Select **Workspace** tooview hello details of hello OMS workspace linked toothis Automation account.</span></span>

## <a name="listing-management-solutions"></a><span data-ttu-id="31c83-165">목록 관리 솔루션</span><span class="sxs-lookup"><span data-stu-id="31c83-165">Listing management solutions</span></span>
<span data-ttu-id="31c83-166">Hello 다음 hello 작업 공간 연결 된 Azure 구독 tooyour 프로시저 tootooview hello 관리 솔루션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-166">Use hello following procedure tootooview hello management solutions in hello workspaces linked tooyour Azure subscription.</span></span>

1. <span data-ttu-id="31c83-167">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-167">Log in toohello Azure portal.</span></span>
2. <span data-ttu-id="31c83-168">Hello 왼쪽된 창에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-168">In hello left pane, select **More services**.</span></span>
3. <span data-ttu-id="31c83-169">너무 아래로 스크롤하여 하나**솔루션** 또는 형식 *솔루션* hello에 **필터** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="31c83-169">Either scroll down too**Solutions** or type *solutions* into hello **Filter** dialog.</span></span>
4. <span data-ttu-id="31c83-170">모든 작업 영역에 설치된 솔루션이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-170">Solutions installed in all your workspaces will be listed.</span></span>

<span data-ttu-id="31c83-171">Note hello OMS 포털을 사용 하 여 hello 현재 작업 영역에 설치 된 유일한 hello Microsoft 솔루션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-171">Note that you can view only hello Microsoft solutions installed in hello current workspace using hello OMS portal.</span></span>

## <a name="removing-a-management-solution"></a><span data-ttu-id="31c83-172">관리 솔루션 제거</span><span class="sxs-lookup"><span data-stu-id="31c83-172">Removing a management solution</span></span>
<span data-ttu-id="31c83-173">관리 솔루션 제거 되 면 hello 솔루션의 모든 리소스 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-173">When a management solution is removed, all resources in hello solution are also removed.</span></span>  

1. <span data-ttu-id="31c83-174">Hello Azure의에서 hello 솔루션을 찾아의 hello 절차를 사용 하 여 포털 [솔루션 나열](#listing-solutions)합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-174">Locate hello solution in hello Azure portal using hello procedure in [Listing solutions](#listing-solutions).</span></span>
2. <span data-ttu-id="31c83-175">Tooremove hello 솔루션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-175">Select hello solution you want tooremove.</span></span>
3. <span data-ttu-id="31c83-176">Hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-176">Click hello **Delete** button.</span></span>

## <a name="creating-a-management-solution"></a><span data-ttu-id="31c83-177">관리 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="31c83-177">Creating a management solution</span></span>
<span data-ttu-id="31c83-178">관리 솔루션 만들기에 대한 전체 지침은 [OMS(Operations Management Suite)](operations-management-suite-solutions-creating.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-178">Complete guidance on creating management solutions are available at [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31c83-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31c83-179">Next steps</span></span>
* <span data-ttu-id="31c83-180">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-180">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
* <span data-ttu-id="31c83-181">자신만의 [관리 솔루션](operations-management-suite-solutions-creating.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31c83-181">Create your own [management solutions](operations-management-suite-solutions-creating.md).</span></span>


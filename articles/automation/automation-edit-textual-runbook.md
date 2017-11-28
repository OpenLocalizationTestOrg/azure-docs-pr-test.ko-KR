---
title: "Azure 자동화의 aaaEditing 텍스트 runbook"
description: "이 문서에서는 hello 텍스트 편집기를 사용 하 여 Azure 자동화의 PowerShell 및 PowerShell 워크플로 runbook 작업에 대 한 절차가 다릅니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a><span data-ttu-id="29920-103">Azure 자동화에서 텍스트 Runbook 편집</span><span class="sxs-lookup"><span data-stu-id="29920-103">Editing textual runbooks in Azure Automation</span></span>
<span data-ttu-id="29920-104">hello Azure 자동화의 텍스트 편집기 수 사용된 tooedit [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) 및 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-104">hello textual editor in Azure Automation can be used tooedit [PowerShell runbooks](automation-runbook-types.md#powershell-runbooks) and [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="29920-105">이 hello 다른 코드 편집기의 intellisense에서 코드 색상 지정 추가 특수 기능 tooassist 사용 하면 일반적인 toorunbooks 리소스에 액세스 등의 일반적인 기능.</span><span class="sxs-lookup"><span data-stu-id="29920-105">This has hello typical features of other code editors such as intellisense and color coding  with additional special features tooassist you in accessing resources common toorunbooks.</span></span>  <span data-ttu-id="29920-106">이 문서에서는 이 편집기를 사용하여 다양한 기능을 수행하기 위한 상세 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-106">This article provides detailed steps for performing different functions with this editor.</span></span>

<span data-ttu-id="29920-107">runbook에 작업, 자산, 및 자식 runbook에 대 한 기능 tooinsert 코드를 포함 하는 hello 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-107">hello textual editor includes a feature tooinsert code for activities, assets, and child runbooks into a runbook.</span></span> <span data-ttu-id="29920-108">직접 입력 하지 않고 hello 코드, 사용 가능한 리소스 목록에서 선택 하 고 hello 적절 한 코드가 hello runbook에 삽입 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-108">Rather than typing in hello code yourself, you can select from a list of available resources and have hello appropriate code inserted into hello runbook.</span></span>

<span data-ttu-id="29920-109">Azure 자동화의 각 Runbook에는 초안과 게시 등 두 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-109">Each runbook in Azure Automation has two versions, Draft and Published.</span></span> <span data-ttu-id="29920-110">Hello runbook의 초안 버전 hello 편집한 다음 실행할 수 있도록 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-110">You edit hello Draft version of hello runbook and then publish it so it can be executed.</span></span> <span data-ttu-id="29920-111">hello 게시 됨 버전은 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-111">hello Published version cannot be edited.</span></span> <span data-ttu-id="29920-112">자세한 내용은 [Runbook 게시](automation-creating-importing-runbook.md#publishing-a-runbook) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29920-112">See [Publishing a runbook](automation-creating-importing-runbook.md#publishing-a-runbook) for more information.</span></span>

<span data-ttu-id="29920-113">와 toowork [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks), 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-113">toowork with [Graphical Runbooks](automation-runbook-types.md#graphical-runbooks), see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="29920-114">tooedit hello Azure 포털을 사용 하 여 runbook</span><span class="sxs-lookup"><span data-stu-id="29920-114">tooedit a runbook with hello Azure portal</span></span>
<span data-ttu-id="29920-115">다음 프로시저 tooopen hello 텍스트 편집기에서 편집할 runbook hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-115">Use hello following procedure tooopen a runbook for editing in hello textual editor.</span></span>

1. <span data-ttu-id="29920-116">Hello Azure 포털에서에서 자동화 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-116">In hello Azure portal, select your automation account.</span></span>
2. <span data-ttu-id="29920-117">Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-117">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="29920-118">Hello 이름을 클릭 hello runbook의 tooedit을 누른 다음 hello **편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-118">Click hello name of hello runbook you want tooedit and then click hello **Edit** button.</span></span>
4. <span data-ttu-id="29920-119">Hello 필요한 편집을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-119">Perform hello required editing.</span></span>
5. <span data-ttu-id="29920-120">편집이 완료되면 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-120">Click **Save** when your edits are complete.</span></span>
6. <span data-ttu-id="29920-121">클릭 **게시** hello hello runbook toobe 게시의 최신 초안 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-121">Click **Publish** if you want hello latest draft version of hello runbook toobe published.</span></span>

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a><span data-ttu-id="29920-122">tooinsert runbook에는 cmdlet</span><span class="sxs-lookup"><span data-stu-id="29920-122">tooinsert a cmdlet into a runbook</span></span>
1. <span data-ttu-id="29920-123">Hello hello 텍스트 편집기의 캔버스에서에서 tooplace hello cmdlet 저장할 hello 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-123">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello cmdlet.</span></span>
2. <span data-ttu-id="29920-124">Hello 확장 **Cmdlet** hello 라이브러리 컨트롤에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="29920-124">Expand hello **Cmdlets** node in hello Library control.</span></span>
3. <span data-ttu-id="29920-125">원하는 toouse hello cmdlet을 포함 하는 hello 모듈을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-125">Expand hello module containing hello cmdlet you want toouse.</span></span>
4. <span data-ttu-id="29920-126">Hello cmdlet tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-126">Right click hello cmdlet tooinsert and select **Add toocanvas**.</span></span>  <span data-ttu-id="29920-127">Hello cmdlet에 둘 이상의 매개 변수를 설정한 경우 기본 집합 hello 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-127">If hello cmdlet has more than one parameter set, then hello default set will be added.</span></span>  <span data-ttu-id="29920-128">또한 hello cmdlet tooselect 다른 매개 변수를 확장할 수 있습니다 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-128">You can also expand hello cmdlet tooselect a different parameter set.</span></span>
5. <span data-ttu-id="29920-129">hello 코드 hello cmdlet에 대 한 매개 변수 전체 목록을 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-129">hello code for hello cmdlet is inserted with its entire list of parameters.</span></span>
6. <span data-ttu-id="29920-130">모든 필수 매개 변수에 대해 중괄호 <>로 묶은 hello 데이터 형식 자리에 해당 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-130">Provide an appropriate value in place of hello data type surrounded by braces <> for any required parameters.</span></span>  <span data-ttu-id="29920-131">필요가 없는 매개 변수는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-131">Remove any parameters you don't need.</span></span>

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a><span data-ttu-id="29920-132">runbook에는 자식 runbook에 대 한 tooinsert 코드</span><span class="sxs-lookup"><span data-stu-id="29920-132">tooinsert code for a child runbook into a runbook</span></span>
1. <span data-ttu-id="29920-133">Hello hello 텍스트 편집기의 캔버스에서에서의 위치를 hello 커서 tooplace hello 코드 hello에 대 한 [자식 runbook](automation-child-runbooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-133">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello code for hello [child runbook](automation-child-runbooks.md).</span></span>
2. <span data-ttu-id="29920-134">Hello 확장 **Runbook** hello 라이브러리 컨트롤에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="29920-134">Expand hello **Runbooks** node in hello Library control.</span></span>
3. <span data-ttu-id="29920-135">Hello runbook tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-135">Right click hello runbook tooinsert and select **Add toocanvas**.</span></span>
4. <span data-ttu-id="29920-136">모든 runbook 매개 변수에 대 한 모든 자리 표시자와 hello 자식 runbook에 대 한 hello 코드 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-136">hello code for hello child runbook is inserted with any placeholders for any runbook parameters.</span></span>
5. <span data-ttu-id="29920-137">각 매개 변수에 대해 적절 한 값으로 hello 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-137">Replace hello placeholders with appropriate values for each parameter.</span></span>

### <a name="tooinsert-an-asset-into-a-runbook"></a><span data-ttu-id="29920-138">runbook에 자산 tooinsert</span><span class="sxs-lookup"><span data-stu-id="29920-138">tooinsert an asset into a runbook</span></span>
1. <span data-ttu-id="29920-139">Hello hello 텍스트 편집기의 캔버스에서에서 원하는 위치 tooplace hello 코드 hello 자식 runbook에 대 한 hello 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-139">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello code for hello child runbook.</span></span>
2. <span data-ttu-id="29920-140">Hello 확장 **자산** hello 라이브러리 컨트롤에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="29920-140">Expand hello **Assets** node in hello Library control.</span></span>
3. <span data-ttu-id="29920-141">Hello 유형의 원하는 자산에 대 한 hello 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-141">Expand hello node for hello type of asset you want.</span></span>
4. <span data-ttu-id="29920-142">Hello 자산 tooinsert 마우스 오른쪽 단추로 클릭 하 고 선택 **toocanvas 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-142">Right click hello asset tooinsert and select **Add toocanvas**.</span></span>  <span data-ttu-id="29920-143">에 대 한 [변수 자산](automation-variables.md), 중 하나를 선택 **"변수 가져오기" toocanvas 추가** 또는 **"변수 설정" toocanvas 추가** 있는지에 따라 원하는 tooget hello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-143">For [variable assets](automation-variables.md), select either **Add "Get Variable" toocanvas** or **Add "Set Variable" toocanvas** depending on whether you want tooget or set hello variable.</span></span>
5. <span data-ttu-id="29920-144">hello 자산에 대 한 hello 코드 hello runbook에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-144">hello code for hello asset is inserted into hello runbook.</span></span>

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="29920-145">tooedit hello Azure 포털을 사용 하 여 runbook</span><span class="sxs-lookup"><span data-stu-id="29920-145">tooedit a runbook with hello Azure portal</span></span>
<span data-ttu-id="29920-146">다음 프로시저 tooopen hello 텍스트 편집기에서 편집할 runbook hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-146">Use hello following procedure tooopen a runbook for editing in hello textual editor.</span></span>

1. <span data-ttu-id="29920-147">Hello Azure 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-147">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="29920-148">선택 hello **Runbook** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-148">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="29920-149">Hello 이름을 클릭 hello runbook의 tooedit 한 다음 선택 hello **작성자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-149">Click hello name of hello runbook you want tooedit and then select hello **Author** tab.</span></span>
4. <span data-ttu-id="29920-150">Hello 클릭 **편집** hello hello 화면 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-150">Click hello **Edit** button at hello bottom of hello screen.</span></span>
5. <span data-ttu-id="29920-151">Hello 필요한 편집을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-151">Perform hello required editing.</span></span>
6. <span data-ttu-id="29920-152">편집이 완료되면 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-152">Click **Save** when your edits are complete.</span></span>
7. <span data-ttu-id="29920-153">클릭 **게시** hello hello runbook toobe 게시의 최신 초안 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-153">Click **Publish** if you want hello latest draft version of hello runbook toobe published.</span></span>

### <a name="tooinsert-an-activity-into-a-runbook"></a><span data-ttu-id="29920-154">Runbook에 활동 tooinsert</span><span class="sxs-lookup"><span data-stu-id="29920-154">tooinsert an activity into a Runbook</span></span>
1. <span data-ttu-id="29920-155">Hello hello 텍스트 편집기의 캔버스에서에서 원하는 tooplace hello 활동 위치 hello 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-155">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello activity.</span></span>
2. <span data-ttu-id="29920-156">Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-156">At hello bottom of hello screen, click **Insert** and then **Activity**.</span></span>
3. <span data-ttu-id="29920-157">Hello에 **통합 모듈** 열, hello 활동을 포함 하는 select hello 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-157">In hello **Integration Module** column, select hello module that contains hello activity.</span></span>
4. <span data-ttu-id="29920-158">Hello에 **활동** 창에서 활동을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-158">In hello **Activity** pane, select an activity.</span></span>
5. <span data-ttu-id="29920-159">Hello에 **설명** 열 hello 활동의 참고 hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-159">In hello **Description** column, note hello description of hello activity.</span></span> <span data-ttu-id="29920-160">자세히 보기를 클릭 하면 필요에 따라 toolaunch 도움말 hello 활동 hello 브라우저에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="29920-160">Optionally, you can click View detailed help toolaunch help for hello activity in hello browser.</span></span>
6. <span data-ttu-id="29920-161">Hello 오른쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-161">Click hello right arrow.</span></span>  <span data-ttu-id="29920-162">Hello 활동 매개 변수가 있으면 정보용 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-162">If hello activity has parameters, they will be listed for your information.</span></span>
7. <span data-ttu-id="29920-163">Hello 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-163">Click hello check button.</span></span>  <span data-ttu-id="29920-164">코드 toorun hello 활동 hello runbook에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-164">Code toorun hello activity will be inserted into hello runbook.</span></span>
8. <span data-ttu-id="29920-165">Hello 활동에 매개 변수가 필요한 경우 중괄호 <>로 묶은 hello 데이터 형식 자리에 적절 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-165">If hello activity requires parameters, provide an appropriate value in place of hello data type surrounded by braces <>.</span></span>

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a><span data-ttu-id="29920-166">runbook에는 자식 runbook에 대 한 tooinsert 코드</span><span class="sxs-lookup"><span data-stu-id="29920-166">tooinsert code for a child runbook into a runbook</span></span>
1. <span data-ttu-id="29920-167">Hello hello 텍스트 편집기의 캔버스에서에서의 위치를 hello 커서 tooplace hello [자식 runbook](automation-child-runbooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-167">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello [child runbook](automation-child-runbooks.md).</span></span>
2. <span data-ttu-id="29920-168">Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **Runbook**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-168">At hello bottom of hello screen, click **Insert** and then **Runbook**.</span></span>
3. <span data-ttu-id="29920-169">Hello runbook tooinsert hello 가운데 열에서 선택한 hello 오른쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-169">Select hello runbook tooinsert from hello center column and click hello right arrow.</span></span>
4. <span data-ttu-id="29920-170">Hello runbook에 매개 변수가 있으면 정보용 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-170">If hello runbook has parameters, they will be listed for your information.</span></span>
5. <span data-ttu-id="29920-171">Hello 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-171">Click hello check button.</span></span>  <span data-ttu-id="29920-172">코드 toorun hello 선택한 runbook hello 현재 runbook에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-172">Code toorun hello selected runbook will be inserted into hello current runbook.</span></span>
6. <span data-ttu-id="29920-173">Hello runbook에 매개 변수가 필요한 경우 중괄호 <>로 묶은 hello 데이터 형식 자리에 적절 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-173">If hello runbook requires parameters, provide an appropriate value in place of hello data type surrounded by braces <>.</span></span>

### <a name="tooinsert-an-asset-into-a-runbook"></a><span data-ttu-id="29920-174">runbook에 자산 tooinsert</span><span class="sxs-lookup"><span data-stu-id="29920-174">tooinsert an asset into a runbook</span></span>
1. <span data-ttu-id="29920-175">Hello hello 텍스트 편집기의 캔버스에서에서 tooplace hello 활동 tooretrieve hello 자산 저장할 hello 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-175">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello activity tooretrieve hello asset.</span></span>
2. <span data-ttu-id="29920-176">Hello 화면 아래쪽에 hello, 클릭 **삽입** 차례로 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-176">At hello bottom of hello screen, click **Insert** and then **Setting**.</span></span>
3. <span data-ttu-id="29920-177">Hello에 **설정 작업** 열, 선택 hello 원하는 동작을 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-177">In hello **Setting Action** column, select hello action that you want.</span></span>
4. <span data-ttu-id="29920-178">Hello hello 가운데 열의 사용 가능한 자산 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-178">Select from hello available assets in hello center column.</span></span>
5. <span data-ttu-id="29920-179">Hello 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-179">Click hello check button.</span></span>  <span data-ttu-id="29920-180">Tooget 코드 또는 집합 hello 자산 hello runbook에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-180">Code tooget or set hello asset will be inserted into hello runbook.</span></span>

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a><span data-ttu-id="29920-181">Windows PowerShell을 사용 하 여 Azure 자동화 runbook tooedit</span><span class="sxs-lookup"><span data-stu-id="29920-181">tooedit an Azure Automation runbook using Windows PowerShell</span></span>
<span data-ttu-id="29920-182">runbook tooedit Windows PowerShell과 함께 hello 원하는 편집기를 사용 하 고이 tooa.ps1 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-182">tooedit a runbook with Windows PowerShell, you use hello editor of your choice and save it tooa .ps1 file.</span></span> <span data-ttu-id="29920-183">Hello를 사용할 수 있습니다 [Get-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) hello runbook의 cmdlet tooretrieve hello 내용을 다음 [Set-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello 기존 초안 runbook hello로 하나를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-183">You can use hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve hello contents of hello runbook and then [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello existing draft runbook with hello modified one.</span></span>

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="29920-184">tooRetrieve hello Runbook Using Windows PowerShell의 내용</span><span class="sxs-lookup"><span data-stu-id="29920-184">tooRetrieve hello Contents of a Runbook Using Windows PowerShell</span></span>
<span data-ttu-id="29920-185">다음 명령 예제는 hello tooretrieve hello runbook에 대 한 스크립트 하 고 tooa 스크립트 파일을 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29920-185">hello following sample commands show how tooretrieve hello script for a runbook and save it tooa script file.</span></span> <span data-ttu-id="29920-186">이 예제에서는 hello 초안 버전이 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29920-186">In this example, hello Draft version is retrieved.</span></span> <span data-ttu-id="29920-187">또한 hello runbook의 가능한 tooretrieve hello 게시 됨 버전 있지만이 버전을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29920-187">It is also possible tooretrieve hello Published version of hello runbook although this version cannot be changed.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="29920-188">tooChange hello Runbook Using Windows PowerShell의 내용</span><span class="sxs-lookup"><span data-stu-id="29920-188">tooChange hello Contents of a Runbook Using Windows PowerShell</span></span>
<span data-ttu-id="29920-189">hello 다음 샘플 명령은 표시 방법을 tooreplace hello 스크립트 파일의 hello 콘텐츠로 runbook의 기존 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-189">hello following sample commands show how tooreplace hello existing contents of a runbook with hello contents of a script file.</span></span> <span data-ttu-id="29920-190">참고 동일 hello는이 예제에서 같이 프로시저 [tooimport Windows powershell 스크립트 파일에서 runbook](automation-creating-importing-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29920-190">Note that this is hello same sample procedure as in [tooimport a runbook from a script file with Windows PowerShell](automation-creating-importing-runbook.md).</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a><span data-ttu-id="29920-191">관련 문서</span><span class="sxs-lookup"><span data-stu-id="29920-191">Related articles</span></span>
* [<span data-ttu-id="29920-192">Azure 자동화에서 Runbook 만들기 또는 가져오기</span><span class="sxs-lookup"><span data-stu-id="29920-192">Creating or importing a runbook in Azure Automation</span></span>](automation-creating-importing-runbook.md)
* [<span data-ttu-id="29920-193">PowerShell 워크플로 학습</span><span class="sxs-lookup"><span data-stu-id="29920-193">Learning PowerShell workflow</span></span>](automation-powershell-workflow.md)
* [<span data-ttu-id="29920-194">Azure 자동화에서 그래픽 작성</span><span class="sxs-lookup"><span data-stu-id="29920-194">Graphical authoring in Azure Automation</span></span>](automation-graphical-authoring-intro.md)
* [<span data-ttu-id="29920-195">인증서</span><span class="sxs-lookup"><span data-stu-id="29920-195">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="29920-196">연결</span><span class="sxs-lookup"><span data-stu-id="29920-196">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="29920-197">자격 증명</span><span class="sxs-lookup"><span data-stu-id="29920-197">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="29920-198">일정</span><span class="sxs-lookup"><span data-stu-id="29920-198">Schedules</span></span>](automation-schedules.md)
* [<span data-ttu-id="29920-199">변수</span><span class="sxs-lookup"><span data-stu-id="29920-199">Variables</span></span>](automation-variables.md)

---
title: "aaaCreating 또는 Azure 자동화에서 runbook 가져오기"
description: "이 문서에서는 설명 방법을 toocreate 파일에서 가져오기 또는 Azure 자동화에서 새 runbook 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a><span data-ttu-id="082e3-103">Azure Automation에서 Runbook 만들기 또는 가져오기</span><span class="sxs-lookup"><span data-stu-id="082e3-103">Creating or importing a runbook in Azure Automation</span></span>
<span data-ttu-id="082e3-104">runbook tooAzure 자동화를 추가할 수 있습니다 [을 새로 만드는](#creating-a-new-runbook) 하거나 hello 또는 파일에서 기존 runbook을 가져와 [Runbook 갤러리](automation-runbook-gallery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-104">You can add a runbook tooAzure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from hello [Runbook Gallery](automation-runbook-gallery.md).</span></span> <span data-ttu-id="082e3-105">이 문서에서는 파일로부터 Runbook을 만들고 가져오는 것과 관련한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-105">This article provides information on creating and importing runbooks from a file.</span></span>  <span data-ttu-id="082e3-106">모든 액세스 커뮤니티 runbook 및 모듈에 대 한 hello 세부 정보를 얻을 수 [Azure 자동화 용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-106">You can get all of hello details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>

## <a name="creating-a-new-runbook"></a><span data-ttu-id="082e3-107">새 Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="082e3-107">Creating a new runbook</span></span>
<span data-ttu-id="082e3-108">Hello Azure 중 하나를 사용 하 여 Azure 자동화에서 새 runbook을 만들 수 있습니다 포털 또는 Windows PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-108">You can create a new runbook in Azure Automation using one of hello Azure portals or Windows PowerShell.</span></span> <span data-ttu-id="082e3-109">Hello runbook을 만든 후에 정보를 사용 하 여 편집할 수 있습니다 [학습 PowerShell 워크플로](automation-powershell-workflow.md) 및 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-109">Once hello runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="082e3-110">toocreate hello Azure 클래식 포털을 사용 하 여 새 Azure 자동화 runbook</span><span class="sxs-lookup"><span data-stu-id="082e3-110">toocreate a new Azure Automation runbook with hello Azure Classic portal</span></span>
<span data-ttu-id="082e3-111">만 처리할 수 있는 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="082e3-111">You can only work with [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks) in hello Azure portal.</span></span>

1. <span data-ttu-id="082e3-112">Hello Azure 클래식 포털에서 클릭 하 고, **새로**, **응용 프로그램 서비스**, **자동화**, **Runbook**, **빨리만들기**.</span><span class="sxs-lookup"><span data-stu-id="082e3-112">In hello Azure Classic portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.</span></span>
2. <span data-ttu-id="082e3-113">Hello 필요한 정보를 입력 한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-113">Enter hello required information, and then click **Create**.</span></span> <span data-ttu-id="082e3-114">hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-114">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
3. <span data-ttu-id="082e3-115">Tooedit hello runbook을 하려는 경우 클릭 **Runbook 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-115">If you want tooedit hello runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="082e3-116">그렇지 않은 경우 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-116">Otherwise, click **OK**.</span></span>
4. <span data-ttu-id="082e3-117">새 runbook hello에 나타납니다. **Runbook** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-117">Your new runbook will appear on hello **Runbooks** tab.</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a><span data-ttu-id="082e3-118">toocreate hello Azure 포털을 사용 하 여 새 Azure 자동화 runbook</span><span class="sxs-lookup"><span data-stu-id="082e3-118">toocreate a new Azure Automation runbook with hello Azure portal</span></span>
1. <span data-ttu-id="082e3-119">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-119">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="082e3-120">Hello 허브에서에서 선택 **Runbook** runbook의 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-120">From hello Hub, select **Runbooks** tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="082e3-121">Hello 클릭 **runbook을 추가할** 단추 차례로 **새 runbook을 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-121">Click on hello **Add a runbook** button and then **Create a new runbook**.</span></span>
4. <span data-ttu-id="082e3-122">입력 **이름** hello runbook 및 선택에 대 한 해당 [형식](automation-runbook-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-122">Type a **Name** for hello runbook and select its [Type](automation-runbook-types.md).</span></span> <span data-ttu-id="082e3-123">hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-123">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
5. <span data-ttu-id="082e3-124">클릭 **만들기** toocreate hello runbook 및 열기 hello 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-124">Click **Create** toocreate hello runbook and open hello editor.</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a><span data-ttu-id="082e3-125">Windows PowerShell을 사용 하 여 새 Azure 자동화 runbook toocreate</span><span class="sxs-lookup"><span data-stu-id="082e3-125">toocreate a new Azure Automation runbook with Windows PowerShell</span></span>
<span data-ttu-id="082e3-126">Hello를 사용할 수 있습니다 [새로 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate 빈 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-126">You can use hello [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="082e3-127">Hello를 지정 하거나 **이름** toocreate 매개 변수는 비어 있는 runbook 나중에 편집할 수 있습니다, 또는 hello를 지정할 수 있습니다 **경로** 매개 변수 tooimport runbook 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-127">You can either specify hello **Name** parameter toocreate an empty runbook that you can later edit, or you can specify hello **Path** parameter tooimport a runbook file.</span></span> <span data-ttu-id="082e3-128">hello **형식** 매개 변수 포함된 toospecify 4 hello runbook 형식 중 하나 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-128">hello **Type** parameter should also be included toospecify one of hello four runbook types.</span></span>

<span data-ttu-id="082e3-129">hello 다음 샘플 명령은 표시 방법을 toocreate 새 빈 runbook 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-129">hello following sample commands show how toocreate a new empty runbook.</span></span>

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a><span data-ttu-id="082e3-130">파일의 Runbook을 Azure Automation으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="082e3-130">Importing a runbook from a file into Azure Automation</span></span>
<span data-ttu-id="082e3-131">PowerShell 스크립트나 PowerShell 워크플로(.ps1 확장명) 또는 내보낸된 그래픽 Runbook(.graphrunbook)을 Azure Automation에 가져와서 새 Runbook을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-131">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension) or an exported graphical runbook (.graphrunbook).</span></span>  <span data-ttu-id="082e3-132">Hello를 지정 해야 [runbook의 형식을](automation-runbook-types.md) 고려 사항에 따라 계정 hello를 고려 하는 hello 가져오기에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-132">You must specify hello [type of runbook](automation-runbook-types.md) that will be created from hello import taking into account hello following considerations.</span></span>

* <span data-ttu-id="082e3-133">.graphrunbook 파일은 새 [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks)에만 가져올 수 있으며 그래픽 Runbook은 .graphrunbook 파일을 통해서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-133">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span></span>
* <span data-ttu-id="082e3-134">PowerShell 워크플로를 포함하는.ps1 파일은 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)에만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-134">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="082e3-135">Hello 파일에 여러 PowerShell 워크플로 있으면 hello 가져오기가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-135">If hello file contains multiple PowerShell Workflows, then hello import will fail.</span></span> <span data-ttu-id="082e3-136">각 워크플로 tooits 직접 파일을 저장 하며 개별적으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-136">You must save each workflow tooits own file and import each separately.</span></span>
* <span data-ttu-id="082e3-137">워크플로를 포함하지 않은 .ps1 파일은 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 또는 [PowerShell Workflow Runbook](automation-runbook-types.md#powershell-workflow-runbooks)으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-137">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="082e3-138">변환 된 tooa 워크플로 됩니다 하 고 주석을 hello 변경 된 내용이 지정 하는 hello runbook에 포함 될 것에 PowerShell 워크플로 runbook으로 가져오므로 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-138">If it is imported into a PowerShell Workflow runbook, then it will be converted tooa workflow, and comments will be included in hello runbook specifying hello changes that were made.</span></span>

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a><span data-ttu-id="082e3-139">tooimport hello Azure 클래식 포털을 통한 파일에서 runbook</span><span class="sxs-lookup"><span data-stu-id="082e3-139">tooimport a runbook from a file with hello Azure Classic portal</span></span>
<span data-ttu-id="082e3-140">Azure 자동화로 프로시저 tooimport 스크립트 파일을 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-140">You can use hello following procedure tooimport a script file into Azure Automation.</span></span>  <span data-ttu-id="082e3-141">이 포털을 사용하는 PowerShell 워크플로 Runbook에만 .ps1 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-141">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using this portal.</span></span>  <span data-ttu-id="082e3-142">다른 형식에 대 한 hello Azure 포털을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-142">You must use hello Azure portal for other types.</span></span>

1. <span data-ttu-id="082e3-143">Hello Azure 관리 포털에서 선택 **자동화** 선택한 다음 자동화 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-143">In hello Azure Management portal, select **Automation** and then select an Automation Account.</span></span>
2. <span data-ttu-id="082e3-144">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-144">Click **Import**.</span></span>
3. <span data-ttu-id="082e3-145">클릭 **파일 찾아보기** hello 스크립트 파일 tooimport 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-145">Click **Browse for File** and locate hello script file tooimport.</span></span>
4. <span data-ttu-id="082e3-146">Tooedit hello runbook을 하려는 경우 클릭 **Runbook 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-146">If you want tooedit hello runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="082e3-147">그렇지 않은 경우 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-147">Otherwise, click OK.</span></span>
5. <span data-ttu-id="082e3-148">새 runbook hello hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-148">hello new runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>
6. <span data-ttu-id="082e3-149">수행 해야 [hello runbook을 게시](#publishing-a-runbook) 전에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-149">You must [publish hello runbook](#publishing-a-runbook) before you can run it.</span></span>

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a><span data-ttu-id="082e3-150">Azure 포털 hello로 파일에서 runbook tooimport</span><span class="sxs-lookup"><span data-stu-id="082e3-150">tooimport a runbook from a file with hello Azure portal</span></span>
<span data-ttu-id="082e3-151">Azure 자동화로 프로시저 tooimport 스크립트 파일을 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-151">You can use hello following procedure tooimport a script file into Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="082e3-152">참고 hello 포털을 사용 하는 PowerShell 워크플로 runbook에.ps1 파일을만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-152">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using hello portal.</span></span>
> 
> 

1. <span data-ttu-id="082e3-153">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="082e3-154">Hello 허브에서에서 선택 **Runbook** runbook의 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-154">From hello Hub, select **Runbooks** tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="082e3-155">Hello 클릭 **runbook을 추가할** 단추 차례로 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-155">Click on hello **Add a runbook** button and then **Import**.</span></span>
4. <span data-ttu-id="082e3-156">클릭 **Runbook 파일** tooselect hello 파일 tooimport</span><span class="sxs-lookup"><span data-stu-id="082e3-156">Click **Runbook file** tooselect hello file tooimport</span></span>
5. <span data-ttu-id="082e3-157">경우 hello **이름** hello 옵션 toochange 있는 다음 필드를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-157">If hello **Name** field is enabled, then you have hello option toochange it.</span></span>  <span data-ttu-id="082e3-158">hello runbook 이름은 문자로 시작 해야 하며 문자, 숫자, 밑줄 및 대시만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-158">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
6. <span data-ttu-id="082e3-159">hello [runbook 형식](automation-runbook-types.md) 이 자동으로 선택 되지만 hello 형식 hello 해당 제한을 고려해를 만든 후 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-159">hello [runbook type](automation-runbook-types.md) will be automatically selected, but you can change hello type after taking hello applicable restrictions into account.</span></span> 
7. <span data-ttu-id="082e3-160">새 runbook hello hello 자동화 계정에 대 한 runbook의 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-160">hello new runbook will appear in hello list of runbooks for hello Automation Account.</span></span>
8. <span data-ttu-id="082e3-161">수행 해야 [hello runbook을 게시](#publishing-a-runbook) 전에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-161">You must [publish hello runbook](#publishing-a-runbook) before you can run it.</span></span>

> [!NOTE]
> <span data-ttu-id="082e3-162">그래픽 runbook 또는 그래픽 PowerShell 워크플로 runbook을 가져온 후 hello 옵션 tooconvert toohello 다른 형식이 있을 경우.</span><span class="sxs-lookup"><span data-stu-id="082e3-162">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have hello option tooconvert toohello other type if wanted.</span></span> <span data-ttu-id="082e3-163">Tootextual을 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-163">You can’t convert tootextual.</span></span>
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a><span data-ttu-id="082e3-164">Windows powershell 스크립트 파일에서 runbook tooimport</span><span class="sxs-lookup"><span data-stu-id="082e3-164">tooimport a runbook from a script file with Windows PowerShell</span></span>
<span data-ttu-id="082e3-165">Hello를 사용할 수 있습니다 [가져오기 AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport PowerShell 워크플로 runbook 초안으로 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-165">You can use hello [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport a script file as a draft PowerShell Workflow runbook.</span></span> <span data-ttu-id="082e3-166">Hello를 사용 하지 않는 한 hello 가져오기 작업이 실패 hello runbook이 이미 있으면 *-Force* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-166">If hello runbook already exists, hello import will fail unless you use hello *-Force* parameter.</span></span> 

<span data-ttu-id="082e3-167">hello 다음 샘플 명령은 runbook에 tooimport 스크립트 파일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-167">hello following sample commands show how tooimport a script file into a runbook.</span></span>

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a><span data-ttu-id="082e3-168">Runbook 게시</span><span class="sxs-lookup"><span data-stu-id="082e3-168">Publishing a runbook</span></span>
<span data-ttu-id="082e3-169">새 Runbook을 만들거나 가져올 때는 게시해야 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-169">When you create or import a new runbook, you must publish it before you can run it.</span></span>  <span data-ttu-id="082e3-170">Automation의 각 Runbook에는 초안 버전과 게시된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-170">Each runbook in Automation has a Draft and a Published version.</span></span> <span data-ttu-id="082e3-171">Hello 게시 됨 버전만 실행 하는 사용 가능한 toobe 이며 hello 초안 버전만 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-171">Only hello Published version is available toobe run, and only hello Draft version can be edited.</span></span> <span data-ttu-id="082e3-172">hello 게시 됨 버전이 모든 변경 내용 toohello 초안 버전의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-172">hello Published version is unaffected by any changes toohello Draft version.</span></span> <span data-ttu-id="082e3-173">Hello 초안 버전을 설정 해야 사용할 수 있는 경우 다음 게시 하면을 hello 초안 버전으로 hello 게시 됨 버전을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-173">When hello Draft version should be made available, then you publish it which overwrites hello Published version with hello Draft version.</span></span>

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a><span data-ttu-id="082e3-174">hello Azure 클래식 포털을 사용 하 여 runbook a toopublish</span><span class="sxs-lookup"><span data-stu-id="082e3-174">toopublish a runbook using hello Azure Classic portal</span></span>
1. <span data-ttu-id="082e3-175">Hello Azure 클래식 포털의 hello runbook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-175">Open hello runbook in hello Azure Classic portal.</span></span>
2. <span data-ttu-id="082e3-176">Hello 화면의 hello 위쪽 클릭 **작성자**합니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-176">At hello top of hello screen, click **Author**.</span></span>
3. <span data-ttu-id="082e3-177">Hello 화면 아래쪽에 hello, 클릭 **게시** 차례로 **예** toohello 확인 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-177">At hello bottom of hello screen, click **Publish** and then **Yes** toohello verification message.</span></span>

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a><span data-ttu-id="082e3-178">hello Azure 포털을 사용 하 여 runbook a toopublish</span><span class="sxs-lookup"><span data-stu-id="082e3-178">toopublish a runbook using hello Azure portal</span></span>
1. <span data-ttu-id="082e3-179">Hello Azure 포털에서에서 hello runbook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-179">Open hello runbook in hello Azure portal.</span></span>
2. <span data-ttu-id="082e3-180">Hello 클릭 **편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-180">Click hello **Edit** button.</span></span>
3. <span data-ttu-id="082e3-181">Hello 클릭 **게시** 단추 차례로 **예** toohello 확인 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-181">Click hello **Publish** button and then **Yes** toohello verification message.</span></span>

## <a name="toopublish-a-runbook-using-windows-powershell"></a><span data-ttu-id="082e3-182">Windows PowerShell을 사용 하 여 runbook toopublish</span><span class="sxs-lookup"><span data-stu-id="082e3-182">toopublish a runbook using Windows PowerShell</span></span>
<span data-ttu-id="082e3-183">Hello를 사용할 수 있습니다 [게시 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish Windows PowerShell로 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-183">You can use hello [Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish a runbook with Windows PowerShell.</span></span> <span data-ttu-id="082e3-184">hello 다음 샘플 명령은 표시 방법을 toopublish 샘플 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="082e3-184">hello following sample commands show how toopublish a sample runbook.</span></span>

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a><span data-ttu-id="082e3-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="082e3-185">Next Steps</span></span>
* <span data-ttu-id="082e3-186">toolearn hello Runbook 및 PowerShell 모듈 갤러리에서 얻을 수 있는 방법에 대 한 참조 [Azure 자동화 용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)</span><span class="sxs-lookup"><span data-stu-id="082e3-186">toolearn about how you can benefit from hello Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span></span>
* <span data-ttu-id="082e3-187">텍스트 편집기를 사용 하 여 PowerShell 및 PowerShell 워크플로 runbook 편집에 대 한 더 toolearn 참조 [Azure 자동화의 텍스트 runbook 편집](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="082e3-187">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span>
* <span data-ttu-id="082e3-188">그래픽 runbook 제작에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="082e3-188">toolearn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>


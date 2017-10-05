---
title: "Azure Automation에서 Runbook 만들기 또는 가져오기"
description: "이 문서에서는 Azure Automation에서 새 Runbook을 만들거나 파일에서 가져오는 방법을 설명합니다."
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
ms.openlocfilehash: 0264de12caaf62e976673a423df731ad27ab01e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a><span data-ttu-id="400da-103">Azure Automation에서 Runbook 만들기 또는 가져오기</span><span class="sxs-lookup"><span data-stu-id="400da-103">Creating or importing a runbook in Azure Automation</span></span>
<span data-ttu-id="400da-104">[새로 만들거나](#creating-a-new-runbook) [파일 또는 Runbook 갤러리에서 기존 Runbook](automation-runbook-gallery.md)을 가져와서 Azure Automation에 Runbook을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-104">You can add a runbook to Azure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from the [Runbook Gallery](automation-runbook-gallery.md).</span></span> <span data-ttu-id="400da-105">이 문서에서는 파일로부터 Runbook을 만들고 가져오는 것과 관련한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-105">This article provides information on creating and importing runbooks from a file.</span></span>  <span data-ttu-id="400da-106">[Azure Automation에 대한 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)에서 커뮤니티 Runbook과 모듈 액세스에 대한 모든 상세 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-106">You can get all of the details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>

## <a name="creating-a-new-runbook"></a><span data-ttu-id="400da-107">새 Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="400da-107">Creating a new runbook</span></span>
<span data-ttu-id="400da-108">Azure Portal 또는 Windows PowerShell 중 하나를 사용하여 Azure Automation에서 새 Runbook을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-108">You can create a new runbook in Azure Automation using one of the Azure portals or Windows PowerShell.</span></span> <span data-ttu-id="400da-109">Runbook를 만든 후에는 [PowerShell 워크플로 학습](automation-powershell-workflow.md) 및 [Azure Automation에서 그래픽 제작](automation-graphical-authoring-intro.md)의 정보를 사용하여 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-109">Once the runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="400da-110">Azure 클래식 포털에서 새 Azure Automation Runbook을 만들려면</span><span class="sxs-lookup"><span data-stu-id="400da-110">To create a new Azure Automation runbook with the Azure Classic portal</span></span>
<span data-ttu-id="400da-111">Azure Portal에서는 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 을 사용한 작업만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-111">You can only work with [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks) in the Azure portal.</span></span>

1. <span data-ttu-id="400da-112">Azure 클래식 포털에서 **새로 만들기**, **App Services**, **Automation**, **Runbook**, **빨리 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-112">In the Azure Classic portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.</span></span>
2. <span data-ttu-id="400da-113">필요한 정보를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-113">Enter the required information, and then click **Create**.</span></span> <span data-ttu-id="400da-114">Runbook 이름은 문자로 시작해야 하며 문자, 숫자, 언더바, 대시 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-114">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
3. <span data-ttu-id="400da-115">지금 runbook을 편집하려면 **Runbook 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-115">If you want to edit the runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="400da-116">그렇지 않은 경우 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-116">Otherwise, click **OK**.</span></span>
4. <span data-ttu-id="400da-117">새 Runbook이 **Runbook** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="400da-117">Your new runbook will appear on the **Runbooks** tab.</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-portal"></a><span data-ttu-id="400da-118">Azure Portal에서 새 Azure Automation  Runbook을 만들려면</span><span class="sxs-lookup"><span data-stu-id="400da-118">To create a new Azure Automation runbook with the Azure portal</span></span>
1. <span data-ttu-id="400da-119">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-119">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="400da-120">Hub에서 **Runbook**을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-120">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="400da-121">**Runbook 추가** 단추를 클릭하고 **새 Runbook 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-121">Click on the **Add a runbook** button and then **Create a new runbook**.</span></span>
4. <span data-ttu-id="400da-122">Runbook의 **이름** 을 입력하고 [유형](automation-runbook-types.md)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-122">Type a **Name** for the runbook and select its [Type](automation-runbook-types.md).</span></span> <span data-ttu-id="400da-123">Runbook 이름은 문자로 시작해야 하며 문자, 숫자, 언더바, 대시 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-123">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
5. <span data-ttu-id="400da-124">**만들기** 를 클릭하여 Runbook을 만들고 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-124">Click **Create** to create the runbook and open the editor.</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-windows-powershell"></a><span data-ttu-id="400da-125">Windows PowerShell에서 새 Azure Automation Runbook을 만들려면</span><span class="sxs-lookup"><span data-stu-id="400da-125">To create a new Azure Automation runbook with Windows PowerShell</span></span>
<span data-ttu-id="400da-126">[New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet을 사용하여 빈 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-126">You can use the [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet to create an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="400da-127">**Name** 매개 변수를 지정하여 나중에 편집할 빈 Runbook을 만들거나, **Path** 매개 변수를 지정하여 Runbook 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-127">You can either specify the **Name** parameter to create an empty runbook that you can later edit, or you can specify the **Path** parameter to import a runbook file.</span></span> <span data-ttu-id="400da-128">네 가지 Runbook 형식 중 하나를 지정하려면 **Type** 매개 변수도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-128">The **Type** parameter should also be included to specify one of the four runbook types.</span></span>

<span data-ttu-id="400da-129">다음 명령 예제에서는 새로운 빈 Runbook을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="400da-129">The following sample commands show how to create a new empty runbook.</span></span>

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a><span data-ttu-id="400da-130">파일의 Runbook을 Azure Automation으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="400da-130">Importing a runbook from a file into Azure Automation</span></span>
<span data-ttu-id="400da-131">PowerShell 스크립트나 PowerShell 워크플로(.ps1 확장명) 또는 내보낸된 그래픽 Runbook(.graphrunbook)을 Azure Automation에 가져와서 새 Runbook을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-131">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension) or an exported graphical runbook (.graphrunbook).</span></span>  <span data-ttu-id="400da-132">다음 사항을 고려하여 가져오기에서 만들 [Runbook 유형](automation-runbook-types.md) 을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-132">You must specify the [type of runbook](automation-runbook-types.md) that will be created from the import taking into account the following considerations.</span></span>

* <span data-ttu-id="400da-133">.graphrunbook 파일은 새 [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks)에만 가져올 수 있으며 그래픽 Runbook은 .graphrunbook 파일을 통해서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-133">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span></span>
* <span data-ttu-id="400da-134">PowerShell 워크플로를 포함하는.ps1 파일은 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)에만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-134">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="400da-135">파일에 여러 PowerShell 워크플로 있으면 가져오기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-135">If the file contains multiple PowerShell Workflows, then the import will fail.</span></span> <span data-ttu-id="400da-136">각 워크플로를 자체 파일에 저장하 고 각각 개별적으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-136">You must save each workflow to its own file and import each separately.</span></span>
* <span data-ttu-id="400da-137">워크플로를 포함하지 않은 .ps1 파일은 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 또는 [PowerShell Workflow Runbook](automation-runbook-types.md#powershell-workflow-runbooks)으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-137">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="400da-138">PowerShell 워크플로 Runbook에 가져오면 워크플로로 변환되며 Runbook에 적용된 변경 내용을 명시하는 메모가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="400da-138">If it is imported into a PowerShell Workflow runbook, then it will be converted to a workflow, and comments will be included in the runbook specifying the changes that were made.</span></span>

### <a name="to-import-a-runbook-from-a-file-with-the-azure-classic-portal"></a><span data-ttu-id="400da-139">Azure 클래식 포털로 파일에서 Runbook을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="400da-139">To import a runbook from a file with the Azure Classic portal</span></span>
<span data-ttu-id="400da-140">Azure Automation에 스크립트 파일을 가져오려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-140">You can use the following procedure to import a script file into Azure Automation.</span></span>  <span data-ttu-id="400da-141">이 포털을 사용하는 PowerShell 워크플로 Runbook에만 .ps1 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-141">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using this portal.</span></span>  <span data-ttu-id="400da-142">다른 유형에는 Azure Portal을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-142">You must use the Azure portal for other types.</span></span>

1. <span data-ttu-id="400da-143">Azure 관리 포털에서 **Automation**을 선택한 다음 Automation 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-143">In the Azure Management portal, select **Automation** and then select an Automation Account.</span></span>
2. <span data-ttu-id="400da-144">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-144">Click **Import**.</span></span>
3. <span data-ttu-id="400da-145">**파일 찾아보기** 를 클릭하고 가져올 스크립트 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-145">Click **Browse for File** and locate the script file to import.</span></span>
4. <span data-ttu-id="400da-146">지금 runbook을 편집하려면 **Runbook 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-146">If you want to edit the runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="400da-147">그렇지 않은 경우 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-147">Otherwise, click OK.</span></span>
5. <span data-ttu-id="400da-148">이 새 Runbook이 Automation 계정의 **Runbook** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="400da-148">The new runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>
6. <span data-ttu-id="400da-149">실행에 앞서 [Runbook을 게시](#publishing-a-runbook) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-149">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span></span>

### <a name="to-import-a-runbook-from-a-file-with-the-azure-portal"></a><span data-ttu-id="400da-150">Azure Portal을 사용하여 파일에서 Runbook을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="400da-150">To import a runbook from a file with the Azure portal</span></span>
<span data-ttu-id="400da-151">Azure Automation에 스크립트 파일을 가져오려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-151">You can use the following procedure to import a script file into Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="400da-152">이 포털을 사용하는 PowerShell 워크플로 Runbook에만 .ps1 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-152">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using the portal.</span></span>
> 
> 

1. <span data-ttu-id="400da-153">Azure Portal에서 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="400da-154">Hub에서 **Runbook**을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-154">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="400da-155">**Runbook 추가** 단추를 클릭하고 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-155">Click on the **Add a runbook** button and then **Import**.</span></span>
4. <span data-ttu-id="400da-156">**Runbook 파일** 을 클릭하여 가져올 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-156">Click **Runbook file** to select the file to import</span></span>
5. <span data-ttu-id="400da-157">**이름** 필드가 활성화된 경우 변경이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-157">If the **Name** field is enabled, then you have the option to change it.</span></span>  <span data-ttu-id="400da-158">Runbook 이름은 문자로 시작해야 하며 문자, 숫자, 언더바, 대시 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-158">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
6. <span data-ttu-id="400da-159">[Runbook 형식](automation-runbook-types.md) 이 자동으로 선택되지만 해당 제한을 고려한 후에 형식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-159">The [runbook type](automation-runbook-types.md) will be automatically selected, but you can change the type after taking the applicable restrictions into account.</span></span> 
7. <span data-ttu-id="400da-160">새 Runbook이 Automation 계정의Runbook 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="400da-160">The new runbook will appear in the list of runbooks for the Automation Account.</span></span>
8. <span data-ttu-id="400da-161">실행에 앞서 [Runbook을 게시](#publishing-a-runbook) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-161">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span></span>

> [!NOTE]
> <span data-ttu-id="400da-162">그래픽 Runbook 또는 그래픽 PowerShell 워크플로 Runbook을 가져온 후 필요에 따라 다른 형식으로 변환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-162">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have the option to convert to the other type if wanted.</span></span> <span data-ttu-id="400da-163">텍스트로는 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-163">You can’t convert to textual.</span></span>
> 
> 

### <a name="to-import-a-runbook-from-a-script-file-with-windows-powershell"></a><span data-ttu-id="400da-164">Windows PowerShell을 사용하여 스크립트 파일에서 Runbook을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="400da-164">To import a runbook from a script file with Windows PowerShell</span></span>
<span data-ttu-id="400da-165">[Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet을 사용하여 스크립트 파일을 PowerShell 워크플로 Runbook 초안으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-165">You can use the [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet to import a script file as a draft PowerShell Workflow runbook.</span></span> <span data-ttu-id="400da-166">해당 Runbook이 이미 있는 경우 *-Force* 매개 변수를 사용하지 않으면 가져오기에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-166">If the runbook already exists, the import will fail unless you use the *-Force* parameter.</span></span> 

<span data-ttu-id="400da-167">다음 명령 예제는 Runbook에 스크립트 파일을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="400da-167">The following sample commands show how to import a script file into a runbook.</span></span>

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a><span data-ttu-id="400da-168">Runbook 게시</span><span class="sxs-lookup"><span data-stu-id="400da-168">Publishing a runbook</span></span>
<span data-ttu-id="400da-169">새 Runbook을 만들거나 가져올 때는 게시해야 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-169">When you create or import a new runbook, you must publish it before you can run it.</span></span>  <span data-ttu-id="400da-170">Automation의 각 Runbook에는 초안 버전과 게시된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-170">Each runbook in Automation has a Draft and a Published version.</span></span> <span data-ttu-id="400da-171">게시된 버전만 실행할 수 있으며 초안 버전만 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-171">Only the Published version is available to be run, and only the Draft version can be edited.</span></span> <span data-ttu-id="400da-172">초안 버전을 변경해도 게시된 버전은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-172">The Published version is unaffected by any changes to the Draft version.</span></span> <span data-ttu-id="400da-173">초안 버전을 사용할 수 있게 되면 이를 게시합니다. 그러면 초안 버전이 게시된 버전을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="400da-173">When the Draft version should be made available, then you publish it which overwrites the Published version with the Draft version.</span></span>

## <a name="to-publish-a-runbook-using-the-azure-classic-portal"></a><span data-ttu-id="400da-174">Azure 클래식 포털을 사용하여 Runbook을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="400da-174">To publish a runbook using the Azure Classic portal</span></span>
1. <span data-ttu-id="400da-175">Azure 클래식 포털에서 Runbook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-175">Open the runbook in the Azure Classic portal.</span></span>
2. <span data-ttu-id="400da-176">화면 맨 위에서 **작성자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-176">At the top of the screen, click **Author**.</span></span>
3. <span data-ttu-id="400da-177">화면 아래쪽에서 **게시**를 클릭한 다음 확인 메시지에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-177">At the bottom of the screen, click **Publish** and then **Yes** to the verification message.</span></span>

## <a name="to-publish-a-runbook-using-the-azure-portal"></a><span data-ttu-id="400da-178">Azure Portal을 사용하여 Runbook을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="400da-178">To publish a runbook using the Azure portal</span></span>
1. <span data-ttu-id="400da-179">Azure Portal에서 Runbook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="400da-179">Open the runbook in the Azure portal.</span></span>
2. <span data-ttu-id="400da-180">**Edit** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-180">Click the **Edit** button.</span></span>
3. <span data-ttu-id="400da-181">**게시** 단추를 클릭한 다음 확인 메시지에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="400da-181">Click the **Publish** button and then **Yes** to the verification message.</span></span>

## <a name="to-publish-a-runbook-using-windows-powershell"></a><span data-ttu-id="400da-182">Windows PowerShell을 사용하여 Runbook을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="400da-182">To publish a runbook using Windows PowerShell</span></span>
<span data-ttu-id="400da-183">[Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet을 사용하여 Windows PowerShell에서 Runbook을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400da-183">You can use the [Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet to publish a runbook with Windows PowerShell.</span></span> <span data-ttu-id="400da-184">다음 명령 예제에서는 샘플 Runbook을 게시하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="400da-184">The following sample commands show how to publish a sample runbook.</span></span>

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a><span data-ttu-id="400da-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="400da-185">Next Steps</span></span>
* <span data-ttu-id="400da-186">Runbook 및 PowerShell 모듈 갤러리를 활용하는 방법을 알아보려면 [Azure Automation에 대한 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)</span><span class="sxs-lookup"><span data-stu-id="400da-186">To learn about how you can benefit from the Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span></span>
* <span data-ttu-id="400da-187">텍스트 편집기를 사용하여 PowerShell 및 PowerShell 워크플로 Runbook을 편집하는 방법을 알아보려면 [Azure Automation에서 텍스트 Runbook 편집](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="400da-187">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span>
* <span data-ttu-id="400da-188">그래픽 Runbook 작성에 대한 자세한 내용은 [Azure Automation에서 그래픽 제작](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="400da-188">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>


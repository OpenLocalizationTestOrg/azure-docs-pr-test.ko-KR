---
title: "Azure 자동화의 일정 | Microsoft Docs"
description: "자동화 일정은 Azure 자동화에서 Runbook이 자동으로 시작되도록 예약하는 데 사용됩니다. 특정 시간 또는 되풀이 일정에 따라 Runbook을 자동으로 시작할 수 있도록 일정을 만들고 관리하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 140bea93c4563666e8cfdf356eaf87500c1aca8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="3c2be-104">Azure 자동화에서 Runbook 예약</span><span class="sxs-lookup"><span data-stu-id="3c2be-104">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="3c2be-105">Azure 자동화에서 Runbook이 지정된 시간에 시작되도록 예약하려면 해당 Runbook을 하나 이상의 일정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-105">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="3c2be-106">Azure 클래식 포털에서 Runbook 및 Azure Portal에서 Runbook의 경우 한 번 실행하거나 매시간 또는 매일 일정으로 실행되도록 일정을 구성할 수 있습니다. 또한 주별, 월별, 주의 특정 요일이나 월의 며칠 또는 월의 특정 날짜에 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-106">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can also schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="3c2be-107">Runbook을 여러 일정에 연결할 수 있으며, 하나의 일정에 여러 Runbook을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-107">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2be-108">일정은 현재 Azure 자동화 DSC 구성을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-108">Schedules do not currently support Azure Automation DSC configurations.</span></span>
> 
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="3c2be-109">Windows PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="3c2be-109">Windows PowerShell Cmdlets</span></span>
<span data-ttu-id="3c2be-110">다음 테이블의 cmdlet은 Azure 자동화에서 Windows PowerShell을 사용하여 일정을 만들고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-110">The cmdlets in the following table are used to create and manage schedules with Windows PowerShell in Azure Automation.</span></span> <span data-ttu-id="3c2be-111">이러한 cmdlet은 [Azure PowerShell 모듈](/powershell/azure/overview)의 일부로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-111">They ship as part of the [Azure PowerShell module](/powershell/azure/overview).</span></span>

| <span data-ttu-id="3c2be-112">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="3c2be-112">Cmdlets</span></span> | <span data-ttu-id="3c2be-113">설명</span><span class="sxs-lookup"><span data-stu-id="3c2be-113">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3c2be-114">**Azure Resource Manager cmdlet**</span><span class="sxs-lookup"><span data-stu-id="3c2be-114">**Azure Resource Manager cmdlets**</span></span> | |
| [<span data-ttu-id="3c2be-115">Get-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-115">Get-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/get-azurermautomationschedule) |<span data-ttu-id="3c2be-116">일정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-116">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="3c2be-117">New-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-117">New-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/new-azurermautomationschedule) |<span data-ttu-id="3c2be-118">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-118">Creates a new schedule.</span></span> |
| [<span data-ttu-id="3c2be-119">Remove-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-119">Remove-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |<span data-ttu-id="3c2be-120">일정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-120">Removes a schedule.</span></span> |
| [<span data-ttu-id="3c2be-121">Set-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-121">Set-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/set-azurermautomationschedule) |<span data-ttu-id="3c2be-122">기존 일정에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-122">Sets the properties for an existing schedule.</span></span> |
| [<span data-ttu-id="3c2be-123">Get-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-123">Get-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |<span data-ttu-id="3c2be-124">예약된 Runbook을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-124">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="3c2be-125">Register-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-125">Register-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |<span data-ttu-id="3c2be-126">Runbook을 일정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-126">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="3c2be-127">Unregister-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-127">Unregister-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |<span data-ttu-id="3c2be-128">일정에서 Runbook을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-128">Dissociates a runbook from a schedule.</span></span> |
| <span data-ttu-id="3c2be-129">**Azure Service Management cmdlet**</span><span class="sxs-lookup"><span data-stu-id="3c2be-129">**Azure Service Management cmdlets**</span></span> | |
| [<span data-ttu-id="3c2be-130">Get-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-130">Get-AzureAutomationSchedule</span></span>](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-131">일정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-131">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="3c2be-132">New-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-132">New-AzureAutomationSchedule</span></span>](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-133">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-133">Creates a new schedule.</span></span> |
| [<span data-ttu-id="3c2be-134">Remove-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-134">Remove-AzureAutomationSchedule</span></span>](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-135">일정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-135">Removes a schedule.</span></span> |
| [<span data-ttu-id="3c2be-136">Set-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="3c2be-136">Set-AzureAutomationSchedule</span></span>](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-137">기존 일정에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-137">Sets the properties for an existing schedule.</span></span> |
| [<span data-ttu-id="3c2be-138">Get-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-138">Get-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-139">예약된 Runbook을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-139">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="3c2be-140">Register-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-140">Register-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-141">Runbook을 일정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-141">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="3c2be-142">Unregister-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="3c2be-142">Unregister-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="3c2be-143">일정에서 Runbook을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-143">Dissociates a runbook from a schedule.</span></span> |

## <a name="creating-a-schedule"></a><span data-ttu-id="3c2be-144">일정 만들기</span><span class="sxs-lookup"><span data-stu-id="3c2be-144">Creating a schedule</span></span>
<span data-ttu-id="3c2be-145">Azure 포털, 클래식 포털에서 또는 Windows PowerShell을 사용하여 runbook에 대한 새 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-145">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="3c2be-146">Azure 클래식 또는 Azure 포털을 사용하여 Runbook을 일정에 연결할 때 새 일정을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-146">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2be-147">Azure Automation은 새로운 예약된 작업이 실행될 때 Automation 계정에서 최신 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-147">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>  <span data-ttu-id="3c2be-148">자동화하는 프로세스 및 Runbook에 영향을 주지 않으려면 먼저 테스트 전용 Automation 계정으로 일정을 연결한 모든 Runbook을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-148">To avoid impacting your runbooks and the processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing.</span></span>  <span data-ttu-id="3c2be-149">이렇게 하면 예정된 Runbook이 올바르게 작동하는지 계속 확인하고 그렇지 않은 경우 업데이트된 Runbook 버전을 프로덕션으로 마이그레이션하기 전에 추가적으로 문제를 해결하고 필요한 모든 변경 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-149">This will validate your scheduled runbooks continue to work correctly and if not, you can further troubleshoot and apply any changes required before migrating the updated runbook version to production.</span></span>  
>  <span data-ttu-id="3c2be-150">**모듈** 블레이드에서 [Azure 모듈 업데이트](automation-update-azure-modules.md) 옵션을 선택하여 수동으로 업데이트하지 않는 한 Automation 계정은 새 버전의 모듈을 자동으로 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-150">Your Automation account will not automatically get any new versions of modules unless you have updated them manually by selecting the [Update Azure Modules](automation-update-azure-modules.md) option from the **Modules** blade.</span></span> 
>  

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="3c2be-151">Azure 포털에서 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-151">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="3c2be-152">Azure 포털의 자동화 계정에서 **자산** 타일을 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-152">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="3c2be-153">**일정** 타일을 클릭하여 **일정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-153">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="3c2be-154">블레이드의 위쪽에서 **일정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-154">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="3c2be-155">**새 일정** 블레이드에서 **이름**을 입력하고 선택적으로 새 일정에 대한 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-155">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="3c2be-156">**한 번** 또는 **되풀이**를 선택하여 일정이 한 번 실행되는지 또는 되풀이되어 실행되는지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-156">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="3c2be-157">**한 번**을 선택하는 경우 **시작 시간**을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-157">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="3c2be-158">**되풀이**를 선택하는 경우 **시작 시간**을 지정하고 얼마나 자주 runbook을 반복할지 빈도를 **시간**, **일**, **주** 또는 **달**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-158">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="3c2be-159">드롭 다운 목록에서 **주** 또는 **달**을 선택하는 경우 선택하면 **되풀이 옵션**이 블레이드에 나타납니다. **되풀이 옵션** 블레이드가 표시되면 **주**를 선택한 경우 요일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-159">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="3c2be-160">**월**을 선택한 경우 **요일** 또는 달력에서 월의 특정한 날짜를 선택하고 마지막으로 월의 마지막 날에 실행할지 여부를 선택할 수 있습니다. 그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-160">If you selected **month**, you can choose by **weekdays** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="3c2be-161">Azure 클래식 포털에서 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-161">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="3c2be-162">Azure 클래식 포털에서 Automation을 선택한 다음 Automation 계정의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-162">In the Azure classic portal, select Automation and then select the name of an Automation account.</span></span>
2. <span data-ttu-id="3c2be-163">**자산** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-163">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="3c2be-164">창의 아래쪽의 **설정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-164">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="3c2be-165">**일정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-165">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="3c2be-166">**이름**을 입력하고 선택적으로 새 일정에 대한 **설명**을 입력합니다.일정은 **한 번**, **매시간**, **매일**, **매주** 또는 **매월** 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-166">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="3c2be-167">**시작 시간** 을 지정하고 선택한 일정 유형에 따라 다른 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-167">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="3c2be-168">Windows PowerShell을 사용하여 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-168">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="3c2be-169">[New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet을 사용하여 Azure 자동화에서 기존 runbook에 대한 새 일정을 만들거나 [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet을 Azure 포털에서 Runbook에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-169">You can use the [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="3c2be-170">일정을 실행해야 할 일정의 시작 시간 및 빈도를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-170">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="3c2be-171">다음 샘플 명령에서는 Azure Resource Manager cmdlet을 사용하여 매월 15일 및 30일에 일정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-171">The following sample commands show how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="3c2be-172">다음 샘플 명령에서는 Azure 서비스 관리 cmdlet을 사용하여 2015년 1월 20일부터 매일 오후 3시 30분에 실행되는 새 일정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-172">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="3c2be-173">Runbook에 일정 연결</span><span class="sxs-lookup"><span data-stu-id="3c2be-173">Linking a schedule to a runbook</span></span>
<span data-ttu-id="3c2be-174">Runbook을 여러 일정에 연결할 수 있으며, 하나의 일정에 여러 Runbook을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-174">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="3c2be-175">Runbook에 매개 변수가 있는 경우 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-175">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="3c2be-176">필수 매개 변수의 값은 반드시 제공해야 하며, 선택적 매개 변수의 값은 필요에 따라 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-176">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="3c2be-177">이러한 값은 Runbook이 이 일정에 따라 시작할 때마다 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-177">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="3c2be-178">동일한 Runbook을 다른 일정에 연결하고 다른 매개 변수 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-178">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="3c2be-179">Azure 포털을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-179">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="3c2be-180">Azure 포털의 자동화 계정에서 **Runbooks** 타일을 클릭하여 **Runbooks** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-180">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="3c2be-181">예약할 Runbook의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-181">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="3c2be-182">현재 Runbook이 일정에 연결되지 않은 경우 새 일정 만들거나 기존 일정에 연결하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-182">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="3c2be-183">runbook에 매개 변수가 있는 경우 **실행 설정 수정(기본값: Azure)** 옵션을 선택할 수 있고 적절하게 정보를 입력할 수 있는 **매개 변수** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-183">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="3c2be-184">Azure 클래식 포털을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-184">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="3c2be-185">Azure 클래식 포털에서 **Automation**을 선택한 다음 Automation 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-185">In the Azure classic portal, select **Automation** and then click the name of an Automation account.</span></span>
2. <span data-ttu-id="3c2be-186">**Runbook** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-186">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="3c2be-187">예약할 Runbook의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-187">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="3c2be-188">**일정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-188">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="3c2be-189">현재 Runbook이 일정에 연결되지 않은 경우 **새 일정에 연결** 또는 **기존 일정에 연결** 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-189">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="3c2be-190">현재 Runbook이 일정에 연결되어 있는 경우 창 아래쪽의 **연결** 을 클릭하여 이러한 옵션에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-190">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="3c2be-191">Runbook에 매개 변수가 있는 경우 해당 값에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-191">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="3c2be-192">Windows PowerShell을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-192">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="3c2be-193">[Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx)을 사용하여 Azure 포털에서 Runbook에 대한 클래식 runbook 또는 [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet에 일정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-193">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="3c2be-194">Parameters 매개 변수를 사용하여 Runbook의 매개 변수 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-194">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="3c2be-195">매개 변수 값 지정에 대한 자세한 내용은 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c2be-195">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="3c2be-196">다음 샘플 명령에서는 매개 변수를 포함하는 Azure Resource Manager cmdlet을 사용하여 runbook에 일정을 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-196">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
<span data-ttu-id="3c2be-197">다음 샘플 명령에서는 매개 변수를 포함하는 Azure 서비스 관리 cmdlet을 사용하여 일정을 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-197">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a><span data-ttu-id="3c2be-198">일정 해제</span><span class="sxs-lookup"><span data-stu-id="3c2be-198">Disabling a schedule</span></span>
<span data-ttu-id="3c2be-199">일정을 해제하면 연결된 모든 Runbook이 더 이상 해당 일정에 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-199">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="3c2be-200">일정을 수동으로 해제하거나, 일정을 만들 때 빈도를 사용하여 일정에 대한 만료 시간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-200">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="3c2be-201">만료 시간에 도달하면 일정이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-201">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="3c2be-202">Azure 포털에서 일정을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-202">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="3c2be-203">Azure 포털의 자동화 계정에서 **자산** 타일을 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-203">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="3c2be-204">**일정** 타일을 클릭하여 **일정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-204">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="3c2be-205">일정 이름을 클릭하여 해당 세부 정보 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-205">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="3c2be-206">**사용**을 **아니오**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-206">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="3c2be-207">Azure 클래식 포털에서 일정을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-207">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="3c2be-208">Azure 클래식 포털의 일정에 대한 일정 세부 정보 페이지에서 일정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-208">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="3c2be-209">Azure 클래식 포털에서 Automation을 선택한 다음 Automation 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-209">In the Azure classic portal, select Automation and then click the name of an Automation account.</span></span>
2. <span data-ttu-id="3c2be-210">자산 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-210">Select the Assets tab.</span></span>
3. <span data-ttu-id="3c2be-211">일정 이름을 클릭하여 해당 세부 정보 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-211">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="3c2be-212">**사용**을 **아니오**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-212">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="3c2be-213">Windows PowerShell을 사용하여 일정을 해제하려면</span><span class="sxs-lookup"><span data-stu-id="3c2be-213">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="3c2be-214">[Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet을 사용하여 기존 runbook에 대한 기존 일정의 속성을 변경하거나 [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet을 Azure 포털에서 runbook에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-214">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="3c2be-215">일정을 해제하려면 **IsEnabled** 매개 변수에 대해 **false**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-215">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="3c2be-216">다음 샘플 명령에서는 Azure Resource Manager cmdlet을 사용하여 runbook에 일정을 비활성화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-216">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="3c2be-217">다음 샘플 명령에서는 Azure 서비스 관리 cmdlet을 사용하여 일정을 비활성화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c2be-217">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a><span data-ttu-id="3c2be-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c2be-218">Next steps</span></span>
* <span data-ttu-id="3c2be-219">Azure 자동화에서 Runbook을 시작하려면 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="3c2be-219">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 


---
title: "Azure 자동화에서 Runbook 예약 | Microsoft Docs"
description: "특정 시간 또는 되풀이 일정에 따라 Runbook을 자동으로 시작할 수 있도록 Azure 자동화에서 일정을 만드는 방법을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="ebadb-103">Azure 자동화에서 Runbook 예약</span><span class="sxs-lookup"><span data-stu-id="ebadb-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="ebadb-104">Azure 자동화에서 Runbook이 지정된 시간에 시작되도록 예약하려면 해당 Runbook을 하나 이상의 일정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="ebadb-105">Azure 클래식 포털에서 Runbook 및 Azure 포털에서 Runbook의 경우 한 번 실행하거나 매시간 또는 매일 일정으로 실행되도록 일정을 구성할 수 있습니다. 또한 주별, 월별, 주의 특정 요일이나 월의 며칠 또는 월의 특정 날짜에 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="ebadb-106">Runbook을 여러 일정에 연결할 수 있으며, 하나의 일정에 여러 Runbook을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="ebadb-107">일정 만들기</span><span class="sxs-lookup"><span data-stu-id="ebadb-107">Creating a schedule</span></span>
<span data-ttu-id="ebadb-108">Azure 포털, 클래식 포털에서 또는 Windows PowerShell을 사용하여 runbook에 대한 새 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="ebadb-109">Azure 클래식 또는 Azure 포털을 사용하여 Runbook을 일정에 연결할 때 새 일정을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ebadb-110">Runbook과 일정을 연결하는 경우 자동화는 계정에 모듈의 현재 버전을 저장하고 해당 일정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="ebadb-111">즉, 일정을 만들고 모듈을 버전 2.0으로 업데이트할 때 계정에 버전 1.0을 사용하는 모듈이 있는 경우 일정은 계속 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="ebadb-112">업데이트된 모듈 버전을 사용하려면 새 일정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="ebadb-113">Azure 클래식 포털에서 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="ebadb-114">Azure 클래식 포털에서 자동화를 선택한 다음 자동화 계정의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="ebadb-115">**자산** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="ebadb-116">창의 아래쪽의 **설정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="ebadb-117">**일정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="ebadb-118">**이름**을 입력하고 선택적으로 새 일정에 대한 **설명**을 입력합니다.일정은 **한 번**, **매시간**, **매일**, **매주** 또는 **매월** 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="ebadb-119">**시작 시간** 을 지정하고 선택한 일정 유형에 따라 다른 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="ebadb-120">Azure 포털에서 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="ebadb-121">Azure 포털의 자동화 계정에서 **자산** 타일을 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="ebadb-122">**일정** 타일을 클릭하여 **일정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="ebadb-123">블레이드의 위쪽에서 **일정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="ebadb-124">**새 일정** 블레이드에서 **이름**을 입력하고 선택적으로 새 일정에 대한 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="ebadb-125">**한 번** 또는 **되풀이**를 선택하여 일정이 한 번 실행되는지 또는 되풀이되어 실행되는지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="ebadb-126">**한 번**을 선택하는 경우 **시작 시간**을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="ebadb-127">**되풀이**를 선택하는 경우 **시작 시간**을 지정하고 얼마나 자주 runbook을 반복할지 빈도를 **시간**, **일**, **주** 또는 **달**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="ebadb-128">드롭 다운 목록에서 **주** 또는 **달**을 선택하는 경우 선택하면 **되풀이 옵션**이 블레이드에 나타납니다. **되풀이 옵션** 블레이드가 표시되면 **주**를 선택한 경우 요일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="ebadb-129">**달**을 선택한 경우 **요일** 또는 달력에서 월의 특정한 날짜를 선택하고 마지막으로 월의 마지막 날에 실행할지 여부를 선택할 수 있습니다. 그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="ebadb-130">Windows PowerShell을 사용하여 새 일정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="ebadb-131">[New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet을 사용하여 Azure 자동화에서 기존 runbook에 대한 새 일정을 만들거나 [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet을 Azure 포털에서 Runbook에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="ebadb-132">일정을 실행해야 할 일정의 시작 시간 및 빈도를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="ebadb-133">다음 샘플 명령에서는 Azure 서비스 관리 cmdlet을 사용하여 2015년 1월 20일부터 매일 오후 3시 30분에 실행되는 새 일정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="ebadb-134">다음 샘플 명령에서는 Azure Resource Manager cmdlet을 사용하여 매월 15일 및 30일에 일정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="ebadb-135">Runbook에 일정 연결</span><span class="sxs-lookup"><span data-stu-id="ebadb-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="ebadb-136">Runbook을 여러 일정에 연결할 수 있으며, 하나의 일정에 여러 Runbook을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="ebadb-137">Runbook에 매개 변수가 있는 경우 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="ebadb-138">필수 매개 변수의 값은 반드시 제공해야 하며, 선택적 매개 변수의 값은 필요에 따라 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="ebadb-139">이러한 값은 Runbook이 이 일정에 따라 시작할 때마다 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="ebadb-140">동일한 Runbook을 다른 일정에 연결하고 다른 매개 변수 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="ebadb-141">Azure 클래식 포털을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="ebadb-142">Azure 클래식 포털에서 **자동화**를 선택한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="ebadb-143">**Runbook** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="ebadb-144">예약할 Runbook의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="ebadb-145">**일정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="ebadb-146">현재 Runbook이 일정에 연결되지 않은 경우 **새 일정에 연결** 또는 **기존 일정에 연결** 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="ebadb-147">현재 Runbook이 일정에 연결되어 있는 경우 창 아래쪽의 **연결** 을 클릭하여 이러한 옵션에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="ebadb-148">Runbook에 매개 변수가 있는 경우 해당 값에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="ebadb-149">Azure 포털을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="ebadb-150">Azure 포털의 자동화 계정에서 **Runbooks** 타일을 클릭하여 **Runbooks** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="ebadb-151">예약할 Runbook의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="ebadb-152">현재 Runbook이 일정에 연결되지 않은 경우 새 일정 만들거나 기존 일정에 연결하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="ebadb-153">runbook에 매개 변수가 있는 경우 **실행 설정 수정(기본값: Azure)** 옵션을 선택할 수 있고 적절하게 정보를 입력할 수 있는 **매개 변수** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="ebadb-154">Windows PowerShell을 사용하여 Runbook에 일정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="ebadb-155">[Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx)을 사용하여 Azure 포털에서 Runbook에 대한 클래식 runbook 또는 [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet에 일정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="ebadb-156">Parameters 매개 변수를 사용하여 Runbook의 매개 변수 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="ebadb-157">매개 변수 값 지정에 대한 자세한 내용은 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebadb-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="ebadb-158">다음 샘플 명령에서는 매개 변수를 포함하는 Azure 서비스 관리 cmdlet을 사용하여 일정을 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="ebadb-159">다음 샘플 명령에서는 매개 변수를 포함하는 Azure Resource Manager cmdlet을 사용하여 runbook에 일정을 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="ebadb-160">일정 해제</span><span class="sxs-lookup"><span data-stu-id="ebadb-160">Disabling a schedule</span></span>
<span data-ttu-id="ebadb-161">일정을 해제하면 연결된 모든 Runbook이 더 이상 해당 일정에 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="ebadb-162">일정을 수동으로 해제하거나, 일정을 만들 때 빈도를 사용하여 일정에 대한 만료 시간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="ebadb-163">만료 시간에 도달하면 일정이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="ebadb-164">Azure 클래식 포털에서 일정을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="ebadb-165">Azure 클래식 포털의 일정에 대한 일정 세부 정보 페이지에서 일정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="ebadb-166">Azure 클래식 포털에서 자동화를 선택한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="ebadb-167">자산 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="ebadb-168">일정 이름을 클릭하여 해당 세부 정보 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="ebadb-169">**사용**을 **아니오**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="ebadb-170">Azure 포털에서 일정을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="ebadb-171">Azure 포털의 자동화 계정에서 **자산** 타일을 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="ebadb-172">**일정** 타일을 클릭하여 **일정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="ebadb-173">일정 이름을 클릭하여 해당 세부 정보 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="ebadb-174">**사용**을 **아니오**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="ebadb-175">Windows PowerShell을 사용하여 일정을 해제하려면</span><span class="sxs-lookup"><span data-stu-id="ebadb-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="ebadb-176">[Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet을 사용하여 기존 runbook에 대한 기존 일정의 속성을 변경하거나 [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet을 Azure 포털에서 runbook에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="ebadb-177">일정을 해제하려면 **IsEnabled** 매개 변수에 대해 **false**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="ebadb-178">다음 샘플 명령에서는 Azure 서비스 관리 cmdlet을 사용하여 일정을 비활성화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="ebadb-179">다음 샘플 명령에서는 Azure Resource Manager cmdlet을 사용하여 runbook에 일정을 비활성화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebadb-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="ebadb-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ebadb-180">Next steps</span></span>
* <span data-ttu-id="ebadb-181">일정으로 작업하는 방법에 대해 자세히 알아보려면 [Azure 자동화의 일정 자산](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="ebadb-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="ebadb-182">Azure 자동화에서 Runbook을 시작하려면 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="ebadb-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 


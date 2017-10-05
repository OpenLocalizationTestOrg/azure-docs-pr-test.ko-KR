---
title: "Azure Automation에서 Runbook 시작 | Microsoft Docs"
description: "Azure Portal과 Windows PowerShell을 사용하여 Azure Automation에서 Runbook을 시작하고 세부 정보를 제공하는 데 사용할 수 있는 여러 방법을 요약합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="53355-103">Azure Automation에서 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="53355-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="53355-104">다음 표를 통해 특정 시나리오에 가장 적합하게 Azure Automation에서 Runbook을 시작하는 방법을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="53355-105">이 문서에서는 Azure Portal 및 Windows PowerShell을 사용하여 Runbook을 시작하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="53355-106">다른 방법에 대한 자세한 내용은 아래 링크에서 액세스할 수 있는 다른 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="53355-107">**방법**</span><span class="sxs-lookup"><span data-stu-id="53355-107">**METHOD**</span></span> | <span data-ttu-id="53355-108">**특성**</span><span class="sxs-lookup"><span data-stu-id="53355-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="53355-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="53355-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="53355-110">대화형 사용자 인터페이스를 사용하는 간단한 방법</span><span class="sxs-lookup"><span data-stu-id="53355-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="53355-111">단순한 매개 변수 값을 제공하는 양식</span><span class="sxs-lookup"><span data-stu-id="53355-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="53355-112">작업 상태를 쉽게 추적</span><span class="sxs-lookup"><span data-stu-id="53355-112">Easily track job state.</span></span><br> <li><span data-ttu-id="53355-113">Azure 로그온을 사용하여 액세스 인증</span><span class="sxs-lookup"><span data-stu-id="53355-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="53355-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="53355-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="53355-115">Windows PowerShell cmdlet을 사용하여 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="53355-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="53355-116">여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음</span><span class="sxs-lookup"><span data-stu-id="53355-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="53355-117">인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증</span><span class="sxs-lookup"><span data-stu-id="53355-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="53355-118">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="53355-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="53355-119">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="53355-119">Track job state.</span></span><br> <li><span data-ttu-id="53355-120">클라이언트에서 PowerShell cmdlet을 지원해야 함</span><span class="sxs-lookup"><span data-stu-id="53355-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="53355-121">Azure Automation API</span><span class="sxs-lookup"><span data-stu-id="53355-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="53355-122">가장 유연하지만 가장 복잡한 방법</span><span class="sxs-lookup"><span data-stu-id="53355-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="53355-123">HTTP 요청을 수행할 수 있는 모든 사용자 지정 코드에서 호출</span><span class="sxs-lookup"><span data-stu-id="53355-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="53355-124">인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증</span><span class="sxs-lookup"><span data-stu-id="53355-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="53355-125">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="53355-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="53355-126">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="53355-126">Track job state.</span></span> |
| [<span data-ttu-id="53355-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="53355-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="53355-128">단일 HTTP 요청에서 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="53355-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="53355-129">URL의 보안 토큰으로 인증</span><span class="sxs-lookup"><span data-stu-id="53355-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="53355-130">Webhook를 만들 때 지정된 매개 변수 값을 클라이언트에서 재정의할 수 없음</span><span class="sxs-lookup"><span data-stu-id="53355-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="53355-131">Runbook에서 HTTP 요청 세부 정보로 채워진 단일 매개 변수를 정의할 수 있음</span><span class="sxs-lookup"><span data-stu-id="53355-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="53355-132">Webhook URL을 통해 작업 상태를 추적할 수 없음</span><span class="sxs-lookup"><span data-stu-id="53355-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="53355-133">Azure 경고에 응답</span><span class="sxs-lookup"><span data-stu-id="53355-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="53355-134">Azure 경고에 답하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="53355-135">Runbook에 대한 Webhook과 경고 링크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="53355-136">URL의 보안 토큰으로 인증</span><span class="sxs-lookup"><span data-stu-id="53355-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="53355-137">일정</span><span class="sxs-lookup"><span data-stu-id="53355-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="53355-138">매시간, 매일, 매주 또는 매월 일정에 따라 Runbook을 자동으로 시작</span><span class="sxs-lookup"><span data-stu-id="53355-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="53355-139">Azure Portal, PowerShell cmdlet 또는 Azure API를 통해 일정 조작</span><span class="sxs-lookup"><span data-stu-id="53355-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="53355-140">일정에서 사용할 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="53355-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="53355-141">다른 Runbook에서</span><span class="sxs-lookup"><span data-stu-id="53355-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="53355-142">Runbook을 다른 Runbook의 활동으로 사용</span><span class="sxs-lookup"><span data-stu-id="53355-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="53355-143">여러 Runbook에서 사용하는 기능에 유용</span><span class="sxs-lookup"><span data-stu-id="53355-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="53355-144">자식 Runbook에 매개 변수 값을 제공하고 부모 Runbook에서 출력 사용</span><span class="sxs-lookup"><span data-stu-id="53355-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="53355-145">다음 이미지는 Runbook의 수명 주기에서 자세한 단계별 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53355-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="53355-146">Runbook이 Azure Automation에서 시작하는 다른 방법인 Hybrid Runbook Worker에 필요한 구성 요소를 포함하여 Azure Automation Runbook 및 다른 구성 요소 간의 상호 작용을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="53355-147">데이터 센터에서 Automation Runbook의 실행에 대해 알아보려면 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="53355-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook 아키텍처](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="53355-149">Azure Portal을 사용하여 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="53355-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="53355-150">Azure Portal에서 **Automation**을 선택한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="53355-151">허브 메뉴에서 **Runbook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="53355-152">**Runbook** 블레이드에서 Runbook을 선택하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="53355-153">Runbook에 매개 변수가 있는 경우 각 매개 변수에 대한 텍스트 상자와 함께 값을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="53355-154">매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53355-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="53355-155">**작업** 블레이드에서 Runbook 작업의 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="53355-156">Windows PowerShell을 사용하여 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="53355-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="53355-157">[Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) 을 사용하여 Windows PowerShell에서 Runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="53355-158">다음 샘플 코드는 Test-Runbook이라는 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="53355-159">Start-AzureRmAutomationRunbook은 Runbook이 시작된 후 해당 상태를 추적하는 데 사용할 수 있는 작업 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="53355-160">[Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)에서 이 작업 개체를 사용하여 작업 상태를 확인하고 [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx)에서 이 작업 개체를 사용하여 해당 출력을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="53355-161">다음 샘플 코드는 Test-Runbook이라는 Runbook을 시작하고 완료될 때까지 기다린 후 해당 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="53355-162">Runbook에 매개 변수가 필요한 경우 [해시 테이블](http://technet.microsoft.com/library/hh847780.aspx)로 제공해야 합니다. 해시 테이블의 키는 매개 변수 이름과 일치하고 값은 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="53355-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="53355-163">다음 예제에서는 FirstName 및 LastName이라는 두 개의 문자열 매개 변수와 RepeatCount라는 정수 및 Show라는 부울 매개 변수를 사용하여 Runbook을 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53355-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="53355-164">매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53355-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="53355-165">Runbook 매개 변수</span><span class="sxs-lookup"><span data-stu-id="53355-165">Runbook parameters</span></span>
<span data-ttu-id="53355-166">Azure Portal 또는 Windows PowerShell을 사용하여 Runbook을 시작한 경우 Azure Automation 웹 서비스를 통해 지침이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="53355-167">이 서비스는 복잡한 데이터 형식을 가진 매개 변수를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="53355-168">복잡한 매개 변수의 값을 제공해야 하는 경우 [Azure Automation에서 자식 Runbook](automation-child-runbooks.md)에 설명된 대로 다른 Runbook에서 인라인으로 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="53355-169">Azure Automation 웹 서비스는 다음 섹션에 설명된 대로 특정 데이터 형식을 사용하는 매개 변수에 대해 특별한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="53355-170">명명된 값</span><span class="sxs-lookup"><span data-stu-id="53355-170">Named values</span></span>
<span data-ttu-id="53355-171">매개 변수의 데이터 형식이 [object]인 경우 *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*JSON 형식을 사용하여 명명된 값 목록으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="53355-172">이러한 값은 단순한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-172">These values must be simple types.</span></span> <span data-ttu-id="53355-173">Runbook에 각 명명된 값에 해당하는 속성이 있는 [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx)로 매개 변수가 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="53355-174">예를 들어 다음 테스트 Runbook에서는 user라는 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="53355-175">user 매개 변수에 다음 텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="53355-176">그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="53355-177">배열</span><span class="sxs-lookup"><span data-stu-id="53355-177">Arrays</span></span>
<span data-ttu-id="53355-178">매개 변수가 [array] 또는 [string[]]과 같은 배열인 경우 *[Value1,Value2,Value3]* JSON 형식을 사용하여 값 목록으로 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="53355-179">이러한 값은 단순한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-179">These values must be simple types.</span></span>

<span data-ttu-id="53355-180">예를 들어 다음 테스트 Runbook에서는 *user*라는 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="53355-181">user 매개 변수에 다음 텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="53355-182">그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="53355-183">자격 증명</span><span class="sxs-lookup"><span data-stu-id="53355-183">Credentials</span></span>
<span data-ttu-id="53355-184">매개 변수의 데이터 형식이 **PSCredential**인 경우 Azure Automation [자격 증명 자산](automation-credentials.md)의 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="53355-185">Runbook에서 지정한 이름의 자격 증명을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="53355-186">예를 들어 다음 테스트 Runbook에서는 credential이라는 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="53355-187">*My Credential*이라는 자격 증명 자산이 있다고 가정할 경우 user 매개 변수에 다음 텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53355-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="53355-188">자격 증명의 사용자 이름을 *jsmith*라고 가정할 경우 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="53355-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="53355-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53355-189">Next steps</span></span>
* <span data-ttu-id="53355-190">현재 문서의 Runbook 아키텍처는 Hybrid Runbook Worker를 사용하여 Azure 및 온-프레미스에서 리소스를 관리하는 runbook의 대략적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53355-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="53355-191">데이터 센터에서 Automation Runbook의 실행에 대해 알아보려면 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53355-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="53355-192">특정 또는 일반 함수에 대해 다른 Runbook에서 사용될 모듈식 Runbook 만들기에 대한 자세한 내용은 [자식 Runbook](automation-child-runbooks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53355-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

